<script setup>
import BlogPost from './components/BlogPost.vue'
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'
import { ref, computed, onMounted } from 'vue';

const posts = ref([]);

const favorite = ref("");
const postXpage = 10;
const start = ref(0);
const end = ref(postXpage);
const loading = ref(true);

const changeFavorite = (title) => {
  favorite.value = title;
}

const nextPage = () => {
    start.value += postXpage;
    end.value += postXpage;
}

const previousPage = () => {
    start.value -= postXpage;
    end.value -= postXpage;
}

onMounted(() => {
  fetchData();
});

const fetchData = async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
}

const maxLength = computed(() => posts.value.length);
</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div v-else class="container">
    <h1>App</h1>
    <h2>Mis Post Favorito: {{ favorite }}</h2>

    <PaginatePost class="mb-2"
      @nextPage="nextPage"
      @previousPage="previousPage"
      :start="start"
      :end="end"
      :maxLength="maxLength"
    />

    <BlogPost
      v-for="post in posts.slice(start, end)" :key="post.id" 
      :title=post.title
      :id="post.id"
      :body="post.body"
      @changeFavorite="changeFavorite"
      class="mb-2"
    ></BlogPost> 
  </div>

</template>
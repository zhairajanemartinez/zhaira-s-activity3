<template>
  <div class="container">
    <h1>Post List</h1>
    <div v-if="loading">Loading posts...</div>
    <ul v-else>
      <li v-for="post in posts" :key="post.id" class="post-item">
        <h3>{{ post.id }}. {{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      posts: [],
      loading: true
    };
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(res => res.json())
      .then(data => {
        this.posts = data;
        this.loading = false;
      })
      .catch(err => {
        console.error('Error fetching posts:', err);
        this.loading = false;
      });
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}
.post-item {
  margin-bottom: 20px;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}
</style>

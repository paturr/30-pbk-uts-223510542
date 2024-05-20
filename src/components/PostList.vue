<template>
    <div class="posts">
      <h1>Postingan User</h1>
      <select v-model="selectedUser" @change="selectUser">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
      <div v-if="loading" class="loading">Loading...</div>
      <ul v-else-if="filteredPosts.length > 0">
        <li v-for="post in filteredPosts" :key="post.id">
          <h2>{{ post.title }}</h2>
          <p class="post-body">{{ post.body }}</p>
        </li>
      </ul>
      <p v-else>Tidak ada postingan untuk user yang dipilih.</p>
    </div>
  </template>
  
  <script>
  export default {
    props: ['users', 'loading', 'posts', 'selectedUser'],
    computed: {
      filteredPosts() {
        if (this.selectedUser) {
          return this.posts.filter(post => post.userId === this.selectedUser);
        } else {
          return [];
        }
      }
    },
    methods: {
      selectUser() {
        this.$emit('selectUser', this.selectedUser);
      }
    }
  };
  </script>
  
  <style scoped>
  /* Your CSS styles here */
  </style>
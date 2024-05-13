<template>
  <div class="todo-app">
    <header>
      <nav>
        <ul>
          <li @click="activeTab = 'todos'" :class="{ active: activeTab === 'todos' }">Todos</li>
          <li @click="activeTab = 'posts'" :class="{ active: activeTab === 'posts' }">Post</li>
        </ul>
      </nav>
    </header>

    <div v-if="activeTab === 'todos'" class="todos">
      <h1> Kegiatan Sehari-hari </h1>
      <p class="author">create by Fathur Azrahman</p>

      <div class="filter-buttons">
        <button @click="filter = 'all'" :class="{ active: filter === 'all' }">Semua</button>
        <button @click="filter = 'done'" :class="{ active: filter === 'done' }">Selesai</button>
        <button @click="filter = 'pending'" :class="{ active: filter === 'pending' }">Belum Selesai</button>
      </div>

      <input type="text" v-model="newTodo" placeholder="Masukkan item kegiatan baru" />
      <button @click="addTodo">Tambah</button>
      <hr>
      <ul>
        <li v-for="(todo, index) in filteredTodos" :key="index" :class="{ done: todo.done }">
          <input type="checkbox" v-model="todo.done" />
          <span>{{ todo.text }}</span>
          <button @click="removeTodo(index)">Hapus</button>
          <hr>
        </li>
      </ul>
    </div>

    <div v-else-if="activeTab === 'posts'" class="posts">
      <h1>Postingan User</h1>
      <select v-model="selectedUser">
        <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
      </select>
      <ul v-if="posts.length > 0">
        <li v-for="post in filteredPosts" :key="post.id">
          <h2>{{ post.title }}</h2>
          <p class="post-body">{{ post.body }}</p>
        </li>
      </ul>
      <p v-else>Tidak ada postingan untuk user yang dipilih.</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeTab: 'todos',
      newTodo: '',
      todos: [],
      filter: 'all', // 'all', 'done', 'pending'
      users: [],
      posts: [],
      selectedUser: null
    };
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos;
      } else if (this.filter === 'done') {
        return this.todos.filter(todo => todo.done);
      } else if (this.filter === 'pending') {
        return this.todos.filter(todo => !todo.done);
      }
    },
    filteredPosts() {
      if (this.selectedUser) {
        return this.posts.filter(post => post.userId === this.selectedUser);
      } else {
        return [];
      }
    }
  },
  async created() {
    await this.fetchUsers();
  },
  methods: {
    async fetchUsers() {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      this.users = await response.json();
    },
    async fetchPosts() {
      const response = await fetch('https://jsonplaceholder.typicode.com/posts');
      this.posts = await response.json();
    },
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({
          text: this.newTodo,
          done: false,
        });
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
  watch: {
    selectedUser(newVal) {
      if (newVal) {
        this.fetchPosts();
      }
    }
  }
};
</script>
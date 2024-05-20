<template>
    <div class="todos">
      <h1>Kegiatan Sehari-hari</h1>
      <p class="author">created by Fathur Azrahman</p>
  
      <div class="filter-buttons">
        <button @click="filter = 'all'" :class="{ active: filter === 'all' }">Semua</button>
        <button @click="filter = 'done'" :class="{ active: filter === 'done' }">Selesai</button>
        <button @click="filter = 'pending'" :class="{ active: filter === 'pending' }">Belum Selesai</button>
      </div>
  
      <div class="add-todo">
        <input type="text" :value="newTodo" @input="updateNewTodo" placeholder="Masukkan item kegiatan baru" />
        <button @click="addTodo">Tambah</button>
      </div>
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
  </template>
  
  <script>
  export default {
    props: ['todos', 'filter', 'newTodo'],
    methods: {
      updateNewTodo(event) {
        this.$emit('update:newTodo', event.target.value);
      },
      addTodo() {
        this.$emit('addTodo');
      },
      removeTodo(index) {
        this.$emit('removeTodo', index);
      }
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
      }
    }
  };
  </script>
  
  <style scoped>
  /* Your CSS styles here */
  </style>
<template>
  <div class="todo-app">
    <h1>List APK</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="List" />
      <button type="submit" class="primary">Tambahkan</button>
    </form>
    <h2>List</h2>
    <div class="filter-section">
      <button @click="filterTodos('all')" class="filter-btn">Semua</button>
      <button @click="filterTodos('active')" class="filter-btn">Belum</button>
      <button @click="filterTodos('completed')" class="filter-btn">Selesai</button>
    </div>
    <ul class="todo-list">
      <li v-for="(todo, index) in filteredTodos" :key="index">
        <input type="checkbox" v-model="todo.done" />
        <span :class="{ 'done': todo.done }">{{ todo.text }}</span>
        <button @click="removeTodo(index)" class="danger">Hapus</button>
      </li>
    </ul>
    <footer>
      <p></p>
    </footer>
  </div>
</template>



<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
      filter: 'all',
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return;
      }
      this.todos.push({
        text: this.newTodo,
        done: false,
      });
      this.newTodo = '';
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    filterTodos(filterType) {
      this.filter = filterType;
    },
  },
  computed: {
    filteredTodos() {
      switch (this.filter) {
        case 'active':
          return this.todos.filter(todo => !todo.done);
        case 'completed':
          return this.todos.filter(todo => todo.done);
        default:
          return this.todos;
      }
    },
  },
};


</script>

<style>
/* General Styles */
body {
  color: #fff; /* White text color for better contrast */
  font-family: "Arial", sans-serif; /* Sans-serif font */
  margin: 0;
  background-color: #3f51b5; /* Indigo background color */
  background-image: url(/src/assets/6030509.jpg); 
  background: cover;
background-size: cover;
background-repeat: no-repeat;
}

/* Todo List Container */
.todo-app {
  color: #fff;
  max-width: 600px;
  margin: 40px auto;
  padding: 40px;
  border-radius: 20px; /* Rounded border */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* Slightly stronger shadow */
  background-color: rgba(255, 255, 255, 0.1); /* Transparent background */
}

/* Heading */
.todo-app h1 {
  text-align: center;
  color: #ff9800; /* Amber heading color */
  font-size: 2.5rem; /* Larger font size */
  margin-bottom: 30px; /* Increased margin */
}

/* Input Form */
.todo-app form {
  display: flex;
  align-items: center; /* Center-align items */
  margin-bottom: 30px;
}

.todo-app input[type=text] {
  flex: 1;
  padding: 15px 20px;
  font-size: 1.2rem;
  border: none; /* Remove border */
  border-radius: 25px; /* Rounded input */
  outline: none;
  background-color: rgba(255, 255, 255, 0.5); /* Semi-transparent background */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2); /* Slightly stronger shadow */
}

.todo-app button[type=submit] {
  margin-left: 10px;
  padding: 15px 30px;
  font-size: 1.2rem;
  background-color: #ff9800; /* Amber button color */
  color: #fff;
  border: none;
  border-radius: 25px; /* Rounded button */
  outline: none;
  cursor: pointer;
  transition: background-color 0.3s; /* Smooth background color transition */
}

.todo-app button[type=submit]:hover {
  background-color: #ff5722; /* Darker amber color on hover */
}


/* Filter Buttons */
.filter-btn {
  background-color: #dd963f;
  padding: 10px 20px; /* Increase padding for larger buttons */
  margin-right: 10px; /* Add margin between buttons */
  border: 1px solid #922626;
  border-radius: 5px;
  cursor: pointer;
  color: #f8f4f4; /* White text for filter buttons */
}

.danger {
  background-color: #95cdf0; /* Oranye yang lebih terang */
  color: #fff; /* Warna teks putih */
  padding: 10px 20px; /* Padding yang lebih besar */
  border: none; /* Tanpa border */
  border-radius: 5px; /* Sudut yang melengkung */
  cursor: pointer; /* Ubah kursor menjadi pointer saat mengarah ke tombol */
  transition: background-color 0.3s; /* Transisi halus untuk perubahan warna latar belakang */
}

.danger:hover {
  background-color: #bd2424; /* Warna oranye yang lebih gelap saat hover */
}


.done {
  text-decoration: line-through;
  color: #aaa;
}

</style>
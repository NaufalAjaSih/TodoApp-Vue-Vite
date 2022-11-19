<template>
<div class="xl:pl-[40%] xl:pt-24 p-4">
  <div class="block xl:max-w-sm sm:max-w-xs p-6 bg-white border border-gray-200 rounded-lg shadow-md dark:bg-gray-800 dark:border-gray-700">
    <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
      Todo List
    </h5>
    <div class="mb-6 mt-6">
      <input v-model="todo" @keyup.enter="add" type="text" id="base-input" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
    </div>
    <button @click="add" class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
      Add Todo
    </button>
  </div>
  <div class="w-full xl:max-w-sm sm:max-w-xs mt-10 p-4 bg-white border rounded-lg shadow-md sm:p-8 dark:bg-gray-800 dark:border-gray-700">
    <div class="flex items-center justify-between mb-4">
      <h5 class="text-xl font-bold leading-none text-gray-900 dark:text-white">Todo List</h5>
      <h5 class="text-xl leading-none text-gray-900 dark:text-white">Todo: {{ total }}</h5>
    </div>
    <List :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo" />
  </div>
</div>
</template>

<script>
import List from './components/List.vue';
export default {
  components: {
    List
  },
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  computed: {
    total() {
      return this.todos.length
    }
  },
  methods: {
    add() {
      if (this.todo != "") {
        this.todos.unshift({
          activity: this.todo,
          isDone: true,
        });
        this.todo = "";
        this.saveToLocalStorage()
      }
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      })
      this.saveToLocalStorage()
    },
    doneTodo(index) {
      this.todos[index].isDone = !this.todos[index].isDone
      this.saveToLocalStorage()
    },
    saveToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  }
};
</script>

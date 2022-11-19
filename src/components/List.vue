<template>
<div class="flow-root">
  <ul role="list" class="divide-y divide-gray-200 dark:divide-gray-700">
    <li class="py-3 sm:py-4" v-for="(todo, index) in todos" :key="index">
      <div class="flex items-center space-x-4">
        <div class="flex-1 min-w-0">
          <p v-if="todo.isDone" class="text-xl font-medium text-gray-900 truncate dark:text-gray-200">
            {{ todo.activity }}
          </p>
          <del v-else class="text-xl font-medium text-gray-900 truncate dark:text-gray-200">
            {{ todo.activity }}
          </del>
        </div>
        <button v-if="todo.isDone" @click="done(index)" class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-green-700 rounded-lg hover:bg-green-800 focus:ring-4 focus:outline-none focus:ring-green-300 dark:bg-green-600 dark:hover:bg-green-700 dark:focus:ring-green-800">
          Done
        </button>
        <button v-else @click="done(index)" class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-orange-700 rounded-lg hover:bg-orange-800 focus:ring-4 focus:outline-none focus:ring-orange-300 dark:bg-orange-600 dark:hover:bg-orange-700 dark:focus:ring-orange-800">
          Not yet
        </button>
        <button @click="deleteTodos(index)" class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-red-700 rounded-lg hover:bg-red-800 focus:ring-4 focus:outline-none focus:ring-red-300 dark:bg-red-600 dark:hover:bg-red-700 dark:focus:ring-red-800">
          Delete
        </button>
      </div>
    </li>
  </ul>
</div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      default: [],
    }
  },
  methods: {
    deleteTodos(index) {
      this.$emit('deleteTodo', index)
    },
    done(index) {
      this.$emit('doneTodo', index)
    }
  },
}
</script>

<template>
  <div class="container">
    <header>
      <h1>Kelola Kegiatan</h1>
      <p class="subtitle">Catat dan kelola kegiatan harian Anda dengan mudah</p>
    </header>

    <TodoForm @add-todo="addTodo" />
    
    <TodoFilter
      :show-only-active="showOnlyActive"
      @toggle-filter="showOnlyActive = !showOnlyActive"
    />

    <div class="todo-list">
      <EmptyState 
        v-if="filteredTodos.length === 0"
        :has-todos="todos.length > 0"
      />

      <TodoItem
        v-for="(todo, index) in filteredTodos"
        :key="index"
        :todo="todo"
        @toggle-complete="toggleComplete(index)"
        @delete-todo="deleteTodo(index)"
      />
    </div>

    <footer>
      <p>{{ todos.length }} kegiatan | {{ completedCount }} selesai</p>
    </footer>
  </div>
</template>

<script>
import { ref, computed, onMounted } from 'vue'
import TodoForm from './components/TodoForm.vue'
import TodoItem from './components/TodoItem.vue'
import TodoFilter from './components/TodoFilter.vue'
import EmptyState from './components/EmptyState.vue'

export default {
  name: 'App',
  components: {
    TodoForm,
    TodoItem,
    TodoFilter,
    EmptyState
  },
  setup() {
    // State
    const todos = ref([])
    const showOnlyActive = ref(false)

    // Load todos from localStorage
    onMounted(() => {
      const savedTodos = localStorage.getItem('todos')
      if (savedTodos) {
        todos.value = JSON.parse(savedTodos)
      }
    })

    // Save todos to localStorage
    const saveTodos = () => {
      localStorage.setItem('todos', JSON.stringify(todos.value))
    }

    // Computed properties
    const filteredTodos = computed(() => {
      if (showOnlyActive.value) {
        return todos.value.filter(todo => !todo.completed)
      }
      return todos.value
    })

    const completedCount = computed(() => {
      return todos.value.filter(todo => todo.completed).length
    })

    // Methods
    const addTodo = (text) => {
      todos.value.push({
        text,
        completed: false
      })
      saveTodos()
    }

    const toggleComplete = (index) => {
      const todoIndex = todos.value.indexOf(filteredTodos.value[index])
      if (todoIndex !== -1) {
        todos.value[todoIndex].completed = !todos.value[todoIndex].completed
        saveTodos()
      }
    }

    const deleteTodo = (index) => {
      const todoIndex = todos.value.indexOf(filteredTodos.value[index])
      if (todoIndex !== -1) {
        todos.value.splice(todoIndex, 1)
        saveTodos()
      }
    }

    return {
      todos,
      showOnlyActive,
      filteredTodos,
      completedCount,
      addTodo,
      toggleComplete,
      deleteTodo
    }
  }
}
</script>
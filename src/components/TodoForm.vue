<template>
  <form class="todo-form" @submit.prevent="handleSubmit">
    <div class="input-wrapper">
      <input 
        type="text" 
        v-model="newTodo" 
        placeholder="Masukkan kegiatan baru..."
        required
      >
    </div>
    <button type="submit" class="btn-primary">Tambah</button>
  </form>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'TodoForm',
  emits: ['add-todo'],
  setup(props, { emit }) {
    const newTodo = ref('')

    const handleSubmit = () => {
      if (newTodo.value.trim()) {
        emit('add-todo', newTodo.value.trim())
        newTodo.value = ''
      }
    }

    return {
      newTodo,
      handleSubmit
    }
  }
}
</script>

<style scoped>
.todo-form {
  padding: 1.5rem;
  background-color: white;
  border-bottom: 1px solid var(--gray-200);
  display: flex;
  gap: 0.75rem;
}

.input-wrapper {
  flex-grow: 1;
  position: relative;
}

input {
  width: 100%;
  padding: 0.75rem 1rem;
  border: 1px solid var(--gray-300);
  border-radius: 6px;
  font-size: 1rem;
  transition: all 0.2s;
}

input:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.2);
}

button {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 6px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-primary {
  background-color: var(--primary);
  color: white;
}

.btn-primary:hover {
  background-color: var(--primary-hover);
}

@media (max-width: 480px) {
  .todo-form {
    flex-direction: column;
  }
}
</style>
<template>
  <div 
    class="todo-item"
    :class="{ completed: todo.completed }"
  >
    <input 
      type="checkbox" 
      class="todo-checkbox" 
      :checked="todo.completed"
      @change="$emit('toggle-complete')"
    >
    <span class="todo-text">{{ todo.text }}</span>
    <button 
      class="todo-delete" 
      @click="$emit('delete-todo')"
      title="Hapus kegiatan"
    >
      ❌
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  emits: ['toggle-complete', 'delete-todo']
}
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 0.75rem;
  background-color: white;
  border: 1px solid var(--gray-200);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  transition: all 0.2s;
}

.todo-item:hover {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05), 0 1px 3px rgba(0, 0, 0, 0.1);
  transform: translateY(-1px);
}

.todo-checkbox {
  margin-right: 1rem;
  width: 1.25rem;
  height: 1.25rem;
  accent-color: var(--success);
  cursor: pointer;
}

.todo-text {
  flex-grow: 1;
  font-size: 1rem;
  color: var(--gray-700);
  transition: all 0.2s;
}

.completed .todo-text {
  text-decoration: line-through;
  color: var(--gray-600);
  opacity: 0.8;
}

.todo-delete {
  margin-left: 0.5rem;
  background-color: transparent;
  color: var(--gray-600);
  padding: 0.375rem;
  border-radius: 4px;
}

.todo-delete:hover {
  background-color: #fee2e2;
  color: var(--danger);
}
</style>
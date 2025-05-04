<template>
  <div class="filters">
    <button 
      class="filter-toggle" 
      :class="{ active: !showOnlyActive }"
      @click="$emit('toggle-filter', false)"
    >
      Semua
    </button>
    <button 
      class="filter-toggle" 
      :class="{ active: showOnlyActive }"
      @click="$emit('toggle-filter', true)"
    >
      Belum Selesai
    </button>
  </div>
</template>

<script>
export default {
  name: 'TodoFilter',
  props: {
    showOnlyActive: {
      type: Boolean,
      default: false
    }
  },
  emits: ['toggle-filter']
}
</script>

<style scoped>
.filters {
  display: flex;
  justify-content: flex-end;
  padding: 1rem 1.5rem;
  background-color: var(--gray-100);
  border-bottom: 1px solid var(--gray-200);
}

.filter-toggle {
  background-color: transparent;
  border: 1px solid var(--gray-300);
  color: var(--gray-700);
  font-size: 0.875rem;
  padding: 0.5rem 1rem;
}

.filter-toggle.active {
  background-color: var(--primary);
  color: white;
  border-color: var(--primary);
}
</style>
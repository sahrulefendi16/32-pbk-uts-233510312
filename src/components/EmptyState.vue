<template>
    <div class="empty-state">
      <div class="empty-state-icon">📝</div>
      <h3 class="empty-state-text">Tidak ada kegiatan</h3>
      <p class="empty-state-subtext" v-if="!hasTodos">
        Silakan tambahkan kegiatan baru untuk mulai mencatat
      </p>
      <p class="empty-state-subtext" v-else>
        Semua kegiatan telah selesai. Hebat!
      </p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'EmptyState',
    props: {
      hasTodos: {
        type: Boolean,
        default: false
      }
    }
  }
  </script>
  
  <style scoped>
  .empty-state {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 3rem 1rem;
    text-align: center;
    color: var(--gray-600);
  }
  
  .empty-state-icon {
    font-size: 3rem;
    margin-bottom: 1rem;
    opacity: 0.3;
  }
  
  .empty-state-text {
    font-size: 1.1rem;
    margin-bottom: 0.5rem;
  }
  
  .empty-state-subtext {
    font-size: 0.9rem;
    max-width: 300px;
    line-height: 1.5;
  }
  </style>
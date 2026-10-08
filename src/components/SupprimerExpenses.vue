<template>
  <div v-if="expense" class="expense-item">
    <div class="expense-info">
      <h3>{{ expense.title }}</h3>
      <p>Catégorie : {{ expense.category }}</p>
      <p>Montant : {{ expense.amount }} Ar</p>
    </div>
    <button type="button" class="delete-button" @click="confirmDelete">
      Supprimer
    </button>
  </div>
</template>

<script setup>
const props = defineProps({
  expense: {
    type: Object,
    required: true
  }
})
const emit = defineEmits(['delete'])

function confirmDelete() {
  const confirmed = window.confirm(
    `Voulez-vous supprimer la dépense "${props.expense.title}" ?`
  )
  
  if (confirmed) {
    emit('delete', props.expense.id)
  }
}
</script>

<style scoped>
.expense-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  padding: 15px;
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
}
.delete-button {
  padding: 8px 12px;
  color: white;
  background-color: #dc3545;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.delete-button:hover {
  background-color: #b02a37;
}
</style>
<template>
  <div class="expense-list">
    <h2>Liste des dépenses</h2>

    <p v-if="expenses.length === 0">
      Aucune dépense enregistrée.
    </p>

    <div v-else>
      <div
        v-for="expense in expenses"
        :key="expense.id"
        class="expense-card"
      >
        <h3>{{ expense.title }}</h3>

        <p>
          Catégorie : {{ expense.category }}
        </p>

        <p>
          Montant : {{ expense.amount }} Ar
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  expenses: {
    type: Array,
    default: () => []
  }
})
</script>

<style scoped>
.expense-list {
  margin: 20px 0;
}

.expense-card {
  padding: 15px;
  margin-bottom: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.expense-card h3 {
  margin-top: 0;
}

.expense-card p {
  margin: 6px 0;
}
</style>
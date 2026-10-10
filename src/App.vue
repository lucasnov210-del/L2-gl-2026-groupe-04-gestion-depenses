
<script setup>
import { ref, computed } from 'vue'
import ExpenseFilters from './components/expenseFilter.vue'

const categories = [
  'Alimentation',
  'Transport',
  'Logement',
  'Santé',
  'Loisirs'
]

const expenses = ref([
  { id: 1, name: 'Achat de riz', category: 'Alimentation', amount: 5000 },
  { id: 2, name: 'Bus', category: 'Transport', amount: 2000 },
  { id: 3, name: 'Loyer', category: 'Logement', amount: 50000 },
  { id: 4, name: 'Achat de légumes', category: 'Alimentation', amount: 3000 }
])

const selectedCategory = ref('Toutes')

const filteredExpenses = computed(() => {
  if (selectedCategory.value === 'Toutes') {
    return expenses.value
  }

  return expenses.value.filter(
    expense => expense.category === selectedCategory.value
  )
})

const totalExpenses = computed(() => {
  return filteredExpenses.value.reduce(
    (total, expense) => total + expense.amount,
    0
  )
})

function handleFilter(category) {
  selectedCategory.value = category
}
</script>

<template>
  <main class="container">
    <header>
      <h1>Gestion des dépenses personnelles</h1>
      <p class="subtitle">
        Suivez et gérez vos dépenses facilement.
      </p>
    </header>

    <section class="summary">
      <div class="summary-card">
        <span>Total des dépenses affichées</span>
        <strong>{{ totalExpenses.toLocaleString('fr-FR') }} Ar</strong>
      </div>

      <div class="summary-card">
        <span>Nombre de dépenses affichées</span>
        <strong>{{ filteredExpenses.length }}</strong>
      </div>
    </section>

    <section class="content">
      <ExpenseFilters
        :categories="categories"
        @filter="handleFilter"
      />

      <h2>Liste des dépenses</h2>

      <p v-if="filteredExpenses.length === 0" class="empty">
        Aucune dépense dans cette catégorie.
      </p>

      <div v-else class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>Dépense</th>
              <th>Catégorie</th>
              <th>Montant</th>
            </tr>
          </thead>

          <tbody>
            <tr
              v-for="expense in filteredExpenses"
              :key="expense.id"
            >
              <td>{{ expense.name }}</td>
              <td>
                <span class="category-badge">
                  {{ expense.category }}
                </span>
              </td>
              <td class="amount">
                {{ expense.amount.toLocaleString('fr-FR') }} Ar
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <p class="result">
        Total affiché :
        <strong>{{ totalExpenses.toLocaleString('fr-FR') }} Ar</strong>
      </p>
    </section>
  </main>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f3f6fb;
  color: #263247;
}

.container {
  width: min(100% - 32px, 1000px);
  margin: 40px auto;
}

header {
  margin-bottom: 25px;
}

h1 {
  margin-bottom: 8px;
  color: #2457a7;
}

.subtitle {
  color: #68758a;
}

.summary {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
  margin-bottom: 24px;
}

.summary-card,
.content {
  padding: 24px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 3px 12px #2030500d;
}

.summary-card span {
  display: block;
  margin-bottom: 12px;
  color: #68758a;
}

.summary-card strong {
  color: #2457a7;
  font-size: 24px;
}

.content h2 {
  margin-top: 24px;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 14px 12px;
  text-align: left;
  border-bottom: 1px solid #e6eaf0;
}

th {
  background: #edf2fa;
}

.category-badge {
  display: inline-block;
  padding: 5px 9px;
  border-radius: 5px;
  background: #edf2fa;
  color: #2457a7;
}

.amount {
  white-space: nowrap;
  font-weight: bold;
}

.result {
  margin-top: 22px;
  text-align: right;
}

.result strong {
  color: #2457a7;
}

.empty {
  padding: 20px 0;
  color: #68758a;
}

@media (max-width: 600px) {
  .summary {
    grid-template-columns: 1fr;
  }

  .summary-card,
  .content {
    padding: 16px;
  }

  h1 {
    font-size: 24px;
  }
}
</style>
sss
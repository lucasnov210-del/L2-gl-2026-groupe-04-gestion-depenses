<script setup>
  import {ref, computed, watch} from 'vue'
  import ExpenseForm from './components/ExpenseForm.vue'
import ListeExpense from './components/ListeExpense.vue'

  //Charger les dépenses enregistrées
  const savedExpenses = localStorage.getItem("expenses")
      ? JSON.parse(localStorage.getItem("expenses"))
      : [];

  //Liste des dépenses
  const expenses = ref(savedExpenses);

  watch(
    expenses,
      (newExpenses) => {
        localStorage.setItem("expenses", 
          JSON.stringify(newExpenses)
        )
      }, {deep: true}
  )


  function addExpense(depense) {
    const newExpenses = {
      id: Date.now(),
      title: depense.title,
      category: depense.category,
      amount: Number(depense.amount)
    }

    expenses.value.push(newExpenses)
  }

  const deleteExpense = (id) => {
    expenses.value = expenses.value.filter(e => e.id !== id);
  };

  const updateExpense = (updatedExpense) => {
    expenses.value = expenses.value.map(
      e => e.id === updatedExpense.id 
        ? updatedExpense
        : e
    )
  }
  //Calcul auto du total
  const totalExpenses = computed(
    () => expenses.value.reduce(
        (sum, expense) => sum + expense.amount, 0
    )
  )

</script>

<template>
  <main>
    <h1 class="text-3xl text-center mt-4 p-4">Gestion des dépenses personnelle</h1>

    <ExpenseForm @depense-ajoutee="addExpense" />

    <section>

      <ListeExpense
          :expenses="expenses"
          @delete-expense="deleteExpense"
          @update-expense="updateExpense"
      />
      <h3 class="text-2xl font-bold">Total des dépenses: {{ totalExpenses }} Ar</h3>
    </section>
  </main>
</template>


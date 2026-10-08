<script setup>
import { ref } from 'vue'
import ExpenseForm from './components/ExpenseForm.vue'

const depenses = ref([])

function ajouterDepense(depense) {
  depenses.value.push(depense)
}
</script>

<template>
  <main class="container">
    <h1>Gestion des dépenses</h1>
    <p class="intro">Enregistrez et consultez vos dépenses.</p>

    <ExpenseForm @depense-ajoutee="ajouterDepense" />

    <section v-if="depenses.length > 0" class="liste">
      <h2>Liste des dépenses</h2>

      <article
        v-for="(depense, index) in depenses"
        :key="index"
        class="depense-item"
      >
        <div>
          <strong>{{ depense.libelle }}</strong>
          <p>{{ depense.categorie }} — {{ depense.date }}</p>
          <p v-if="depense.description">{{ depense.description }}</p>
        </div>

        <span>{{ depense.montant.toLocaleString('fr-FR') }} Ar</span>
      </article>
    </section>
  </main>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

.container {
  max-width: 720px;
  margin: 40px auto;
  padding: 28px;
  font-family: Arial, sans-serif;
  color: #1f2937;
}

h1 {
  margin-bottom: 4px;
  color: #1d4ed8;
}

.intro {
  margin-top: 0;
  color: #6b7280;
}

.liste {
  margin-top: 28px;
}

.liste h2 {
  color: #1d4ed8;
}

.depense-item {
  display: flex;
  justify-content: space-between;
  gap: 20px;
  margin-top: 12px;
  padding: 16px;
  border-left: 4px solid #2563eb;
  border-radius: 6px;
  background: #eff6ff;
}

.depense-item p {
  margin: 5px 0 0;
  color: #4b5563;
}

.depense-item span {
  font-weight: 700;
  color: #166534;
  white-space: nowrap;
}
</style>
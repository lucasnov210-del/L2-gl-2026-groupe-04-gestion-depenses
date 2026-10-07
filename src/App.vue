<script setup>
import { ref } from 'vue'

const depenses = ref([])

const nouvelleDepense = ref({
  date: '',
  libelle: '',
  categorie: '',
  montant: '',
  description: '',
})

const message = ref('')

function ajouterDepense() {
  if (
    !nouvelleDepense.value.date ||
    !nouvelleDepense.value.libelle ||
    !nouvelleDepense.value.categorie ||
    !nouvelleDepense.value.montant
  ) {
    message.value = 'Veuillez remplir tous les champs obligatoires.'
    return
  }

  depenses.value.push({
    ...nouvelleDepense.value,
    montant: Number(nouvelleDepense.value.montant),
  })

  message.value = 'La dépense a été ajoutée avec succès.'

  nouvelleDepense.value = {
    date: '',
    libelle: '',
    categorie: '',
    montant: '',
    description: '',
  }
}
</script>

<template>
  <main class="container">
    <h1>Gestion des dépenses</h1>
    <p class="intro">Ajouter une nouvelle dépense</p>

    <form class="depense-form" @submit.prevent="ajouterDepense">
      <label for="date">Date *</label>
      <input id="date" v-model="nouvelleDepense.date" type="date" required />

      <label for="libelle">Libellé *</label>
      <input
        id="libelle"
        v-model="nouvelleDepense.libelle"
        type="text"
        placeholder="Exemple : Achat de fournitures"
        required
      />

      <label for="categorie">Catégorie *</label>
      <select id="categorie" v-model="nouvelleDepense.categorie" required>
        <option value="" disabled>Choisir une catégorie</option>
        <option value="Alimentation">Alimentation</option>
        <option value="Transport">Transport</option>
        <option value="Logement">Logement</option>
        <option value="Santé">Santé</option>
        <option value="Loisir">Loisir</option>
        <option value="Autre">Autre</option>
      </select>

      <label for="montant">Montant (Ar) *</label>
      <input
        id="montant"
        v-model="nouvelleDepense.montant"
        type="number"
        min="1"
        placeholder="Exemple : 5000"
        required
      />

      <label for="description">Description</label>
      <textarea
        id="description"
        v-model="nouvelleDepense.description"
        rows="4"
        placeholder="Description facultative"
      ></textarea>

      <button type="submit">Ajouter la dépense</button>
    </form>

    <p v-if="message" class="message">{{ message }}</p>

    <section v-if="depenses.length > 0" class="liste">
      <h2>Liste des dépenses</h2>

      <article v-for="(depense, index) in depenses" :key="index" class="depense-item">
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

.depense-form {
  display: grid;
  gap: 10px;
  margin-top: 24px;
  padding: 24px;
  border: 1px solid #d1d5db;
  border-radius: 10px;
  background: #f9fafb;
}

label {
  font-weight: 600;
}

input,
select,
textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #9ca3af;
  border-radius: 6px;
  font: inherit;
}

button {
  margin-top: 8px;
  padding: 12px;
  border: 0;
  border-radius: 6px;
  background: #2563eb;
  color: white;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
}

button:hover {
  background: #1d4ed8;
}

.message {
  margin-top: 16px;
  padding: 12px;
  border-radius: 6px;
  background: #dcfce7;
  color: #166534;
}

.liste {
  margin-top: 28px;
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
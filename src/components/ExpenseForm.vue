<script setup>
import { ref } from 'vue'

const emit = defineEmits(['depense-ajoutee'])

const libelle = ref('')
const categorie = ref('Alimentation')
const montant = ref('')
const date = ref('')
const description = ref('')
const message = ref('')

function ajouter() {
  message.value = ''

  if (!libelle.value || !montant.value || !date.value) {
    message.value = 'Veuillez remplir le libellé, le montant et la date.'
    return
  }

  const montantNum = Number(montant.value.replace(/s/g, '').replace(',', '.'))
  if (Number.isNaN(montantNum) || montantNum <= 0) {
    message.value = 'Le montant doit être un nombre positif.'
    return
  }

  emit('depense-ajoutee', {
    libelle: libelle.value.trim(),
    categorie: categorie.value,
    montant: montantNum,
    date: date.value,
    description: description.value.trim()
  })

  libelle.value = ''
  categorie.value = 'Alimentation'
  montant.value = ''
  date.value = ''
  description.value = ''

  message.value = 'La dépense a été ajoutée avec succès.'
}
</script>

<template>
  <section class="formulaire">
    <h2>Ajouter une dépense</h2>

    <form @submit.prevent="ajouter">
      <div class="champ">
        <label for="date">Date</label>
        <input id="date" v-model="date" type="date" required />
      </div>

      <div class="champ">
        <label for="libelle">Libellé</label>
        <input id="libelle" v-model="libelle" type="text" required />
      </div>

      <div class="champ">
        <label for="categorie">Catégorie</label>
        <select id="categorie" v-model="categorie">
          <option>Alimentation</option>
          <option>Transport</option>
          <option>Logement</option>
          <option>Santé</option>
          <option>Loisirs</option>
          <option>Autre</option>
        </select>
      </div>

      <div class="champ">
        <label for="montant">Montant (Ar)</label>
        <input id="montant" v-model="montant" type="text" inputmode="decimal" required />
      </div>

      <div class="champ">
        <label for="description">Description (optionnel)</label>
        <textarea id="description" v-model="description" rows="3"></textarea>
      </div>

      <button type="submit">Ajouter la dépense</button>
    </form>

    <p v-if="message" class="message">{{ message }}</p>
  </section>
</template>

<style scoped>
.formulaire {
  max-width: 600px;
  margin: 0 auto 32px;
  padding: 24px;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  background: #f9fafb;
}

.formulaire h2 {
  margin-top: 0;
  color: #1d4ed8;
}

.champ {
  margin-bottom: 16px;
}

.champ label {
  display: block;
  margin-bottom: 6px;
  font-weight: 600;
  color: #374151;
}

.champ input,
.champ select,
.champ textarea {
  width: 100%;
  padding: 8px 10px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 14px;
}

.champ textarea {
  resize: vertical;
}

button {
  padding: 10px 16px;
  border: none;
  border-radius: 6px;
  background: #2563eb;
  color: #fff;
  font-weight: 600;
  cursor: pointer;
}

button:hover {
  background: #1d4ed8;
}

.message {
  margin-top: 12px;
  padding: 8px 12px;
  border-radius: 6px;
  background: #ecfdf5;
  color: #065f46;
}
</style>
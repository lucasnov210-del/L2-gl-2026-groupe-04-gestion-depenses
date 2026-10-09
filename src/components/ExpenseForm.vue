<script setup>
  import { ref } from 'vue'

  const emit = defineEmits(['depense-ajoutee'])

  const libelle = ref('')
  const categorie = ref('Alimentation')
  const montant = ref('')
  const message = ref('')

  function ajouter() {
    message.value= ''

    if(!libelle.value.trim() || !categorie.value || !montant.value) {
      message.value = 'Veuillez remplir tous les champs.'
      return
    }

    const montantNum = Number(montant.value)

    if(!Number.isFinite(montantNum) || montantNum <= 0) {
      message.value = 'Le montant doit être un nombre positif.'
      return
    }

    emit('depense-ajoutee', {
      title: libelle.value.trim(),
      category: categorie.value,
      amount: montantNum
    })

    libelle.value = ''
    categorie.value = 'Alimentation'
    montant.value = ''
    message.value = ''
  }
</script>

<template>
 <section class="max-w-md mx-auto bg-white shadow-md rounded-lg p-6">
  <h2 class="text-2xl font-bold text-gray-800 mb-4">Ajouter une dépense</h2>

  <form @submit.prevent="ajouter" class="space-y-4">
    <div>
      <label for="libelle" class="block text-sm font-medium text-gray-700">Nom de la dépense:</label>
      <input 
        type="text" 
        v-model="libelle"
        id="libelle"
        class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-bleu-500
        focus:ring focus:ring-blue-200 px-3 py-2"
      />
    </div>

    <div>
      <label for="categorie" class="block text-sm font-medium text-gray-700">Catégorie:</label>
      <select 
          id="categorie" 
          v-model="categorie"
          class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-bleu-500
          focus:ring focus:ring-blue-200 px-3 py-2"
        >
        <option value="Alimentation">
          Alimentation
        </option>
        <option value="Transport">
          Transport
        </option>
        <option value="Logement">
          Logement
        </option>
        <option value="Loisirs">
          Loisirs
        </option>
      </select>
    </div>

    <div>
      <label for="montant" class="block text-sm font-medium text-gray-700">Montant:</label>
      <input 
        type="number"
        v-model="montant" 
        id="montant"
        min="1"
        step="any"
        class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-bleu-500
        focus:ring focus:ring-blue-200 px-3 py-2"
      />
    </div>

    <button 
      type="submit"
      class="w-full bg-blue-600 text-white font-semibold py-2 px-4 rounded-md hover:bg-blue-700
      focus:outline-none focus:ring-2 focus:ring-blue-400"
    >
      Ajouter une dépense
    </button>

    <p v-if="message" class="text-red-400">{{ message }}</p>
  </form>
 </section>
</template>
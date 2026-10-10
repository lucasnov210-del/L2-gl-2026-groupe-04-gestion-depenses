
<template>
  <div class="expense-filter">
    <label for="category">Filtrer par catégorie :</label>

    <select
      id="category"
      v-model="selectedCategory"
      @change="emit('filter', selectedCategory)"
    >
      <option value="Toutes">Toutes les catégories</option>

      <option
        v-for="category in categories"
        :key="category"
        :value="category"
      >
        {{ category }}
      </option>
    </select>

    <p v-if="selectedCategory !== 'Toutes'">
      Catégorie sélectionnée : {{ selectedCategory }}
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  categories: {
    type: Array,
    default: () => [
      'Alimentation',
      'Transport',
      'Logement',
      'Santé',
      'Loisirs'
    ]
  }
})

const emit = defineEmits(['filter'])
const selectedCategory = ref('Toutes')
</script>

<style scoped>
.expense-filter {
  margin: 20px 0;
}

label {
  margin-right: 10px;
  font-weight: bold;
}

select {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  background: white;
  cursor: pointer;
}

p {
  margin-top: 10px;
  color: #2457a7;
}
</style>

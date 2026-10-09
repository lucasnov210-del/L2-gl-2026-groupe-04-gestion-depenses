<script setup>
  const props = defineProps({
    expense: {
      type: Object,
      required: true
    }
  });

  const emit = defineEmits(["delete-expense"]);
</script>

<template>
  <button 
    @click="emit('delete-expense', props.expense.id)"
    class="bg-red-600 text-white  py-1 px-3 rounded hover:bg-red-500 "
  >
    Supprimer
  </button>
</template>
<script setup>
import { formatAmount } from '../utils/expenses'

defineProps({
  expense: { type: Object, required: true },
  active: { type: Boolean, default: false },
})
defineEmits(['edit', 'delete'])
</script>

<template>
  <tr :class="{ active }">
    <td>{{ expense.date }}</td>
    <td>{{ expense.description }}</td>
    <td><span class="tag">{{ expense.category }}</span></td>
    <td class="right">{{ formatAmount(expense.amount) }}</td>
    <td class="right">
      <button class="btn small" @click="$emit('edit')">Modifier</button>
      <button class="btn small danger" @click="$emit('delete')">Supprimer</button>
    </td>
  </tr>
</template>

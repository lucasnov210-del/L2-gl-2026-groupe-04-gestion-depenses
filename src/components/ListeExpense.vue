<script setup>
    import SupprimerExpense from "./SupprimerExpenses.vue"
    import ModifierExpense from "./ModifierExpense.vue"
    import { ref, computed } from "vue";

    const props = defineProps({
        expenses: {
            type: Array,
            default: () => []
        }
    });

    const emit = defineEmits(["delete-expense", "update-expense"]);

    const editedExpense = ref(null);

    const selectedCategory = ref("");

    const startEdit = (expense) => {
        editedExpense.value = { ...expense};
    };

    const cancelEdit = () => {
        editedExpense.value = null;
    };

    const saveEdit = (updatedExpense) => {
        emit('update-expense', updatedExpense);
        editedExpense.value = null;
    };

    const filteredExpense = computed(
        () => {
            if(!selectedCategory.value) return props.expenses;
            return props.expenses.filter(e => e.category === selectedCategory.value);
        }
    )
</script>

<template>
    <div class="max-w-2xl mx-auto mt-6">

        <div class="mb-4">
            <label for=""classblock text-sm font-medium text-gray-700>
                Filtrer par catégorie: 
        </label>
        <select v-model="selectedCategory"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm px-3 py-2"
        >
            <option value="Alimentation">Alimentation</option>
            <option value="Transport">Transport</option>
            <option value="Logement">Logement</option>
            <option value="Loisirs">Loisirs</option>
    </select>
    </div>
        <p v-if="filteredExpense.length === 0"
        class="text-center text-gray-500 italic"
        >Aucune dépense enregistrée.</p>
        <ul v-else class="space-y-4">
            <li 
                v-for="expense in filteredExpense"
                :key="expense.id"
                class="bg-white shadow-md rouded-lg p-4 flex flex-col gap-2"
            >

                <div v-if="!editedExpense || editedExpense.id !== expense.id" class="flex justify-between items-center">
                    <h3 class="text-lg font-semibold text-gray-800">{{ expense.title }}</h3>
                    <p class="text-sm text-gray-600">Catégorie:{{ expense.category }}</p>
                    <p class="text-sm text-blue-600 font-medium">Montant:{{ expense.amount }} Ar </p>
                    <SupprimerExpense
                        :expense="expense"
                        @delete-expense="emit('delete-expense', expense.id)"
                    />

                    <button
                        @click="startEdit(expense)"
                        class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded"
                    >
                        Modifier
                    </button>
                </div>

                <ModifierExpense
                    v-else
                    :expense="editedExpense"
                    @save="saveEdit"
                    @cancel="cancelEdit"
                />
            </li>
        </ul>
    </div>
</template>
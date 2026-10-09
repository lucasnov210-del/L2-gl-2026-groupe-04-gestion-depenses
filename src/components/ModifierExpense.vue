<script setup>
    import { ref } from 'vue';

    const props = defineProps({
        expense: {
            type: Object,
            required: true,
            default: () => ({})
        }
    });

    const emit = defineEmits(['save', 'cancel']);

    const libelle = ref(props.expense?.title);
    const categorie = ref(props.expense?.category);
    const montant = ref(props.expense?.amount);

    const save = () => {
        if(!props.expense || !props.expense.id){
            alert("L'ID de la dépense est manquant")
        }
        
        emit("save",{
            id:props.expense.id,
            title: libelle.value,
            category: categorie.value,
            amount: Number(montant.value)
        });
    };
</script>

<template>
    <div>
        <form @submit.prevent="ajouter" class="space-y-4">
            <div>
            <label for="libelle" class="block text-sm font-medium text-gray-700">Nom de la dépense:</label>
            <input 
                type="text" 
                v-model="libelle"
                id="libelle"
                placeholder="Achat du riz..."
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
                placeholder="200000..."
                class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-bleu-500
                focus:ring focus:ring-blue-200 px-3 py-2"
            />
            </div>

                <button @click="save">
                    Enregistrer
                </button>

                <button @click="emit('cancel')">
                    Annuler
                </button>
        </form>
    </div>
</template>
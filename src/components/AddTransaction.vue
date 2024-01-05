<template>
    <h3>Add new Transaction</h3>
    <form action="" id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" v-model="text" placeholder="Entrer du text" id="text" />
        </div>
        <div class="form-control">
            <label for="amount">
                montant <br>
                (negative - expense, positive - income)
            </label>
            <input type="number" v-model="amount" id="amount" placeholder="Entrer un amount" />
        </div>
        <button class="btn">ajouter une transaction</button>
    </form>
</template>

<script setup>
import { ref, } from 'vue';
import { useToast } from 'vue-toastification';
const toast = useToast()
const text = ref('');
//si tu mets une chaine de charactere ça va pas marcher car on attend un chiffre
const amount = ref();

const emit = defineEmits(['transactionSubmitted'])



const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error('Both fields must be filled');
        return;
    }
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    }

    emit("transactionSubmitted", transactionData);
    text.value = '';
    amount.value = '';
};


</script>



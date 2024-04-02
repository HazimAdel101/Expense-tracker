<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
            <label for="amount">Amount <br />
                (negative - expense, positive - income)</label>
            <input type="number" v-model="amount" step="0.01" id="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from "vue-toastification";

const text = ref('');
const amount = ref(0);

const toast = useToast();

const emit = defineEmits(['add-transaction']);

const onSubmit = () => {

    if (!text.value || !amount.value) {
        toast.error('Please add a text and amount');
        return;
    }
    const newTransaction = {
        id: Math.floor(Math.random() * 100000000),
        text: text.value,
        amount: +amount.value
    }

    emit('add-transaction', newTransaction);

    text.value = '';
    amount.value = 0;
}
</script>
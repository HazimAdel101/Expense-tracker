<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpense :income="+income" :expense="+expense" />
    <TransactionList :transactions="transactions" @delete-transaction="deleteTransaction" />
    <AddTransaction @add-transaction="insert" />
  </div>
</template>

<script setup>
import Header from "@/components/Header.vue";
import Balance from "@/components/Balance.vue";
import IncomeExpense from "@/components/IncomeExpense.vue";
import TransactionList from "@/components/TransactionList.vue";
import AddTransaction from "@/components/AddTransaction.vue";

import { useToast } from "vue-toastification";

import { ref, computed } from "vue";

const toast = useToast();

const transactions = ref([
  { id: 1, text: "Flower", amount: -20 },
  { id: 2, text: "Salary", amount: 300 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 }
])

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
})


const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

const insert = (newTransaction) => {
  transactions.value.push({
    id: newTransaction.id,
    text: newTransaction.text,
    amount: newTransaction.amount
  })

  toast.success('Transaction added successfully', {
    timeout: 2000
  })
}

const deleteTransaction = (id) => {
  transactions.value = transactions.value.filter(transaction => transaction.id !== id)

  toast.success('Transaction deleted successfully', {
    timeout: 2000
  })
}

</script>
<template>
  <q-page class="">
    <div class="q-pa-md">
      <q-list bordered separator>
        <q-item v-for="entrie in entries" :key="entrie.id">
          <q-item-section> {{ entrie.name }} </q-item-section>

          <q-item-section side top> {{ currencify(entrie.amount) }} </q-item-section>
        </q-item>
      </q-list>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'

const entries = ref([
  {
    id: 'id0',
    name: 'Rent',
    amount: 20000,
  },
  {
    id: 'id1',
    name: 'Food',
    amount: -4000,
  },
  {
    id: 'id2',
    name: 'Traviling',
    amount: -3000,
  },
  {
    id: 'id3',
    name: 'Rechargr',
    amount: -250,
  },
  {
    id: 'id4',
    name: 'Extra Expenses',
    amount: -2000,
  },
])

function currencify(amount) {
  let posNegSymbol = ''
  if (amount > 0) posNegSymbol = '+'
  else if (amount < 0) posNegSymbol = '-'

  const currencySymbol = '$',
    amountPositive = Math.abs(amount),
    amountFormatted = amountPositive.toLocaleString('en-US', {
      minimumFractionDigits: 2,
      maximumFractionDigits: 2,
    })

  return `${posNegSymbol} ${currencySymbol} ${amountFormatted}`
}

console.log(entries)
</script>

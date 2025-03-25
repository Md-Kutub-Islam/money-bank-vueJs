<template>
  <q-page class="">
    <div class="q-pa-md">
      <q-list bordered separator>
        <q-item v-for="entrie in entries" :key="entrie.id">
          <q-item-section :class="useAmountColorClass(entrie.amount)">
            {{ entrie.name }}
          </q-item-section>

          <q-item-section :class="useAmountColorClass(entrie.amount)" side top>
            {{ useCurrencify(entrie.amount) }}
          </q-item-section>
        </q-item>
      </q-list>
    </div>

    <q-footer class="bg-transparent">
      <div class="row justify-between q-pb-sm q-px-xl q-py-sm text-h6 shadow-up-3">
        <div class="col text-grey-7">Balence:</div>
        <div class="col text-right" :class="useAmountColorClass(balence)">
          {{ useCurrencify(balence) }}
        </div>
      </div>
      <q-form @submit="addEntry" class="row q-px-md q-pb-sm q-col-gutter-sm bg-primary">
        <div class="col">
          <q-input
            ref="nameRef"
            v-model.number="addEntryForm.name"
            type="text"
            input-class="text-right"
            placeholder="Name"
            bg-color="white"
            outlined
            dense
          />
        </div>
        <div class="col">
          <q-input
            v-model="addEntryForm.amount"
            type="number"
            input-class="text-right"
            step="0.01"
            placeholder="Amount"
            bg-color="white"
            outlined
            dense
          />
        </div>
        <div class="col col-auto">
          <q-btn type="submit" color="primary" icon="add" round />
        </div>
      </q-form>
    </q-footer>
  </q-page>
</template>

<script setup>
import { computed, reactive, ref } from 'vue'
import { useCurrencify } from 'src/use/useCurensify'
import { useAmountColorClass } from 'src/use/useAmountColorClass'
import { uid } from 'quasar'

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

const balence = computed(() => {
  return entries.value.reduce((acc, { amount }) => {
    return acc + amount
  }, 0)
})

const nameRef = ref(null)

const addEntryForm = reactive({
  name: '',
  amount: null,
})

const resetForm = () => {
  addEntryForm.name = ''
  addEntryForm.amount = null
  nameRef.value.focus()
}

const addEntry = () => {
  const newEntry = Object.assign({}, addEntryForm, { id: uid() })
  entries.value.push(newEntry)
  resetForm()
}
</script>

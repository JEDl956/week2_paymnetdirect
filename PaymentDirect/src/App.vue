<script setup>
import { ref, computed } from 'vue'
import Header from './components/Header.vue'
import Card from './components/Card.vue'
import Section from './components/Section.vue'

const people = ref([])
const newperson = ref('')

const addPerson = () => {
  const name = newperson.value.trim()
  if (!name) return
  people.value.push(name)
  newperson.value = ''
}

const expenses = ref([])
const newExpense = ref({
  desc: '',
  amount: 0,
  paidBy: ''
})

const addExpense = () => {
  const { desc, amount, paidBy } = newExpense.value
  if (!desc.trim() || isNaN(parseFloat(amount)) || !paidBy) return

  expenses.value.push({
    desc: desc.trim(),
    amount: parseFloat(amount),
    paidBy
  })

  newExpense.value = { desc: '', amount: 0, paidBy: '' }
}

const total = computed(() =>
  expenses.value.reduce((t, e) => t + e.amount, 0).toFixed(2)
)

const split = computed(() => {
  if (people.value.length === 0) return '0.00'
  return (total.value / people.value.length).toFixed(2)
})

const summaryList = computed(() =>
  people.value.map(person => {
    const paid = expenses.value
      .filter(e => e.paidBy === person)
      .reduce((t, e) => t + e.amount, 0)

    const balance = paid - total.value / people.value.length
    return `${person} ${balance >= 0 ? 'gets' : 'owes'} $${Math.abs(balance).toFixed(2)}`
  })
)
</script>

<template>
  <Header />

  <Card>
    <form class="rowForm" @submit.prevent="addPerson">
      <input type="text" placeholder="Add person name" v-model="newperson" />
      <button>Add Person</button>
    </form>

    <form class="rowForm" @submit.prevent="addExpense">
      <input type="text" placeholder="Expense description" v-model="newExpense.desc" />
      <input type="number" placeholder="Amount" v-model="newExpense.amount" />
      <select v-model="newExpense.paidBy">
        <option disabled value="">Paid by</option>
        <option v-for="person in people" :key="person">{{ person }}</option>
      </select>
      <button>Add Expense</button>
    </form>

    <Section title="People">
      <ul class="list">
        <li v-for="person in people" :key="person">{{ person }}</li>
      </ul>
    </Section>

    <Section title="Expenses">
      <ul class="list">
        <li v-for="expense in expenses" :key="expense.desc">
          {{ expense.desc }} - ${{ expense.amount.toFixed(2) }} ({{ expense.paidBy }})
        </li>
      </ul>
    </Section>

    <Section title="Total">
      <p>Total Spent: ${{ total }}</p>
      <p>Split Per Person: ${{ split }}</p>
    </Section>

    <Section title="Summary">
      <ul class="list">
        <li v-for="(item, i) in summaryList" :key="i">{{ item }}</li>
      </ul>
    </Section>
  </Card>
</template>

<style scoped>
.rowForm {
  display: flex;
  gap: 6px;
  margin-bottom: 10px;
}

input,
select {
  border: 1px solid black;
  padding: 6px;
}

button {
  border: 1px solid black;
  background: white;
  padding: 6px 10px;
}

.list {
  list-style: none;
  padding: 0;
}

.list li {
  border: 1px solid black;
  padding: 6px;
  margin-bottom: 6px;
}

p {
  color: black;
}
</style>

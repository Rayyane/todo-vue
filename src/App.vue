<script setup>
import { ref } from 'vue';
import PlanPicker from './components/PlanPicker.vue'

const tasks = ref([
  { id: 1, title: 'buy 10 party hats', completed: false, highPriority: true },
  { id: 2, title: 'buy 1 board game', completed: false, highPriority: true },
  { id: 3, title: 'buy 10 shot glasses', completed: true, highPriority: true },
  { id: 4, title: 'buy 10 disposable plates', completed: false, highPriority: false }
]);



const newTask = ref('');
const highPriority = ref(false);
const msg = ref('hi');
const editing = ref(false)

const doEdit = (e) => {
  editing.value = e
  newTask.value = ""
}

const addTask = () => {
  tasks.value.push({
    id: tasks.value.length + 1,
    title: newTask.value,
    completed: false,
    highPriority: highPriority.value
  })
  newTask.value = '';
  highPriority.value = false;
}

const togglePurchased = (task) => {
  task.completed = !task.completed;
}

</script>

<template>
  <div class="header">
    <h1>Shopping List</h1>
  </div>

  <button v-if="editing" @click="doEdit(false)"> Cancel </button>

  <button v-else @click="doEdit(true)"> Add Item </button>

  <form @submit.prevent="addTask" v-if="editing">

    <input type="text" v-model.trim="newTask" placeholder="Add a new task" />
    <label>High Priority
      <input type="checkbox" v-model="highPriority" />
    </label>

    <button type="submit">Add Task</button>
  </form>

  <div class="shopping-list">
    <div class="card">
      <ul>
        <li v-for="task in tasks" @click="togglePurchased(task)" :key="task.id" :class="[
          task.highPriority ? 'text-alert' : 'text-grey',
          task.completed ? 'strike-through' : 'text-bold text-xl'
        ]">
          {{ task.id }}.
          {{ task.title }}
        </li>
      </ul>
    </div>
  </div>

  <PlanPicker/>

</template>

<style scoped>
ul,
li {
  list-style: none;
  background-color: transparent;
  padding-left: 0;
  margin-left: 10px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #284139;
}

.shopping-list {
  width: 60%;
  margin: 20px auto;
  padding: 20px;
}

.text-alert {
  color: red;
}

.text-grey {
  color: grey;
}

.text-bold {
  font-weight: bold;
}

.text-xl {
  font-size: 1.1rem;
}

.strike-through {
  text-decoration: line-through;
}
</style>

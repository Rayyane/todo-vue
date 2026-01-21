<script setup>
import { ref } from 'vue'
import CoffeePlan from './CoffeePlan.vue'

const plans = ref([
    'The Regular', 'The Addict', 'The Hacker'
])

const fireEvent = (payload) => {
    console.log(payload)
}

</script>

<template>
    <div class="card">
        <ul>
            <CoffeePlan 
            v-for="plan in plans" 
            :key="plan" 
            :name="plan"
            @msg="fireEvent"></CoffeePlan>
        </ul>
    </div>
</template>
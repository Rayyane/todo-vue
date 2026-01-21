<script setup>
    const props = defineProps({
        name: {type: String, default: 'Default Plan'}
    })

    const emit = defineEmits(['msg'])
</script>

<template>
    <div class="card">
        <div class="title" @click="emit('msg', name)"> {{ name }} </div>
    </div>
</template>
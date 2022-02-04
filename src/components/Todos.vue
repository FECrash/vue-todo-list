<script setup lang='ts'>
import {computed} from 'vue'
import Todo from './Todo.vue'
const items = computed(() => {
    return ['hi', 'hello', '!', 'hi', 'hello', '!', '!']
})
</script>
<template>
    <div class="box-border md:box-content mt-2 text-center align-top">
        <Todo v-for="item in items" />
    </div>
</template>

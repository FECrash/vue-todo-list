<script setup lang="ts">
import { computed } from 'vue';
import Todo from './Todo.vue';
const items = computed(() => ['hi', 'hello', '!', 'hi', 'hello', '!', '!']);
</script>
<template>
  <div class="box-border md:box-content mt-2 text-center align-top">
    <Todo v-for="(_, index) in items" :key="index" />
  </div>
</template>

<script setup lang="ts">
import InputForm from './components/InputForm.vue';
import Todos from './components/Todos.vue';
</script>

<template>
  <main class="w-full h-full">
    <div class="body mt-14 px-4 py-8">
      <div class="m-auto" style="width: 1100px">
        <InputForm />
        <Todos />
      </div>
    </div>
  </main>
</template>

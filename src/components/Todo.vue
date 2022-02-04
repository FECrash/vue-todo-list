<script setup lang="ts">
import TodoAction from './TodoAction.vue';
</script>
<template>
  <div class="w-60 mt-2 ml-6 mr-6 p-4 flex flex-col border-2 rounded-lg border-rose-600 float-left">
    <div contentEditable="true">내용</div>
    <TodoAction />
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import MasonryWall from './core/masonry-wall.vue';
import TodoAction from './TodoAction.vue';
const items = computed(() => ['hi', 'hello', '!', 'hi', 'hello', '!', '!']);
</script>
<template>
  <MasonryWall :items="items" :ssr-columns="1" :column-width="350" :gap="16">
    <div class="w-80 p-4 flex flex-col border-2 rounded-lg border-rose-600 float-left">
      <div class="text p-3 break-all mr-6 focus:outline-none" contentEditable="true">내용</div>
      <TodoAction />
    </div>
  </MasonryWall>
</template>

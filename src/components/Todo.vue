<script setup lang="ts">
import MasonryWall from './core/masonry-wall.vue';
import TodoAction from './TodoAction.vue';
import { useStore } from 'vuex';
import { ref } from 'vue';
import { TodoState } from '../store';

const store = useStore();
const items = ref<TodoState[]>([]);
store.subscribe((_, state) => (items.value = [...state.todoList]));

const handleChange = ({ target }: Event, id: string) => {
  const childNodes = (target as HTMLElement).childNodes;
  const cloned = (target as HTMLElement).cloneNode(false);
  Array.from(childNodes)
    .map(child => {
      if (child.nodeType === 3) {
        const $div = document.createElement('div');
        $div.innerText = child.textContent as string;
        return $div;
      }
      if ((child as HTMLElement).innerHTML.trim() === '<br>') {
        return document.createElement('br');
      }
      return child;
    })
    .forEach(node => cloned.appendChild(node));
  const content = (cloned as HTMLElement).innerHTML
    .replace(/<br>/gi, '\n')
    .replace(/<div>.*?<\/div>/gi, (match: string) => `${match}\n`)
    .replace(/<div>|<\/div>/gi, '');
  store.dispatch('sync', { id, content });
};
</script>
<template>
  <MasonryWall :items="items" :column-width="350" :gap="16">
    <template #default="{ item }">
      <div
        class="w-80 p-4 flex flex-col border-2 rounded-lg border-rose-600 float-left"
        :style="{
          backgroundColor: item.noteColor,
          color: item.color,
          textDecoration: item.isFinish ? 'line-through' : '',
        }"
      >
        <div
          class="text p-3 break-all mr-6 focus:outline-none whitespace-pre"
          contentEditable="true"
          @blur="e => handleChange(e, item.id)"
        >
          {{ item.content }}
        </div>
        <TodoAction :item="item" />
      </div>
    </template>
  </MasonryWall>
</template>

<script setup lang="ts">
import MasonryWall from './core/masonry-wall.vue';
import TodoAction from './TodoAction.vue';
import { useStore } from 'vuex';
import { ref } from 'vue';
import { TodoState } from '../store';

const store = useStore();
const items = ref<TodoState[]>([]);
store.subscribe((_, state) => {
  // console.log(state)
  // items.value = [...state.todoList].map(todo => ({ ...todo, content: todo.content.split('\n') }));
  items.value = [...state.todoList];
});

const handleChange = ({ target }: Event, id: string) => {
  const content = (target as HTMLElement).innerText;
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
          class="text p-3 break-all mr-6 focus:outline-none"
          contentEditable="true"
          @blur="e => handleChange(e, item.id)"
        >
          {{ item.content }}
          <!-- <template v-for="(contentText, index2) in item.content" :key="index2">
            {{ contentText }}
            <br v-if="item.content.length !== index2 + 1" />
          </template> -->
        </div>
        <TodoAction :item="item" />
      </div>
    </template>
  </MasonryWall>
</template>

<script setup>
defineProps({
  todo: Object,
  isCompletedTodoList: Boolean,
  id: Number,
});
</script>

<template>
  <li
    v-if="!isCompletedTodoList"
    class="border border-lime-500 p-4 mb-2 rounded-xl text-lg flex justify-between items-center text-lime-500"
  >
    <span>{{ todo.text }}</span>
    <div class="flex">
      <Button @click.prevent="$emit('addTodoInCompleteList', id)"
        ><img src="/complete.png" class="w-6 mr-2"
      /></Button>
      <Button @click.prevent="$emit('removeTodo', id)"
        ><img src="/remove.png" class="w-6"
      /></Button>
    </div>
  </li>
  <li
    v-else
    class="border border-lime-500 p-4 mb-2 rounded-xl text-lg text-white bg-lime-500 text-center"
  >
    <span class="text-center">{{ todo.text }}</span>
  </li>
</template>

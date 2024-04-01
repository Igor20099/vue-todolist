<script setup>
defineProps({
  isCompletedTodoList: Boolean,
});
</script>

<template>
  <div class="flex justify-center mb-8">
    <button
      :class="
        isCompletedTodoList
          ? 'w-1/4 border px-2 py-2 bg-white text-lime-500 transition disabled:bg-slate-300 hover:bg-lime-500 hover:text-white'
          : 'w-1/4 border  px-2 py-2 bg-lime-500 text-white transition disabled:bg-slate-300 '
      "
      @click.prevent="$emit('changeList', false)"
    >
      Текущие
    </button>
    <button
      :class="
        isCompletedTodoList
          ? 'w-1/4 border px-2 py-2 bg-lime-500 text-white transition disabled:bg-slate-300 mr-4'
          : 'w-1/4 border px-2 py-2 bg-white text-lime-500 transition disabled:bg-slate-300 mr-4 hover:bg-lime-500 hover:text-white'
      "
      @click.prevent="$emit('changeList', true)"
    >
      Выполненые
    </button>
  </div>
</template>

<style></style>

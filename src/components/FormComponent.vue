<script setup>
import { ref } from "vue";

const emit = defineEmits(["addTodo"]);

const inputTodo = ref("");

const addTodo = () => {
  emit("addTodo", inputTodo.value);
  inputTodo.value = "";
};
</script>

<template>
  <div class="flex flex-col mb-8">
    <form class="flex justify-between">
      <input
        type="text"
        placeholder="Напишите задачу..."
        class="flex-1 mr-2 border outline-none rounded-md px-2 py-2"
        v-model="inputTodo"
        maxlength="50"
      />
      <Button
        class="border rounded-md px-2 py-2 bg-lime-500 text-white hover:bg-lime-400 transition disabled:bg-slate-300"
        @click.prevent="addTodo"
        :disabled="inputTodo === '' ? true : false"
        >Добавить</Button
      >
    </form>
    <div>
      <span class="text-slate-400"
        >Количество символов: {{ inputTodo.length }}/50</span
      >
    </div>
  </div>
</template>

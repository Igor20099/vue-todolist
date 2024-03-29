<script setup>
import { ref, reactive } from "vue";

const inputTodo = ref("");
const isCompletedTodoList = ref(false);
const todoList = ref([]);

const addTodo = (todo) => {
  todoList.value.push(todo);
};
</script>

<template>
  <div class="w-2/5 m-auto flex flex-col">
    <h1 class="text-center text-6xl font-bold mb-6 uppercase">Список Задач</h1>
    <form class="flex justify-between mb-8">
      <input
        type="text"
        placeholder="Напишите задачу..."
        class="flex-1 mr-2 border outline-none rounded-md px-2 py-2"
        v-model="inputTodo"
        maxlength="50"
      />
      <Button
        class="border rounded-md px-2 py-2 bg-lime-500 text-white hover:bg-lime-400 transition disabled:bg-slate-300"
        @click.prevent="addTodo(inputTodo)"
        :disabled="inputTodo === '' ? true : false"
        >Добавить</Button
      >
    </form>
    <div class="flex justify-center mb-8">
      <button
        :class="
          isCompletedTodoList
            ? 'w-1/4 border rounded-md px-2 py-2 bg-white text-lime-500 transition disabled:bg-slate-300 mr-4 hover:bg-lime-500 hover:text-white'
            : 'w-1/4 border rounded-md px-2 py-2 bg-lime-500 text-white transition disabled:bg-slate-300 mr-4'
        "
        @click.prevent="isCompletedTodoList = false"
      >
        Текущие
      </button>
      <button
        :class="
          isCompletedTodoList
            ? 'w-1/4 border rounded-md px-2 py-2 bg-lime-500 text-white transition disabled:bg-slate-300 mr-4'
            : 'w-1/4 border rounded-md px-2 py-2 bg-white text-lime-500 transition disabled:bg-slate-300 mr-4 hover:bg-lime-500 hover:text-white'
        "
        @click.prevent="isCompletedTodoList = true"
      >
        Выполненые
      </button>
    </div>
    <div>
      <ul class="flex flex-col">
        <li
          :key="i"
          v-for="(todo, i) in todoList"
          class="border border-lime-500 p-4 mb-2 rounded-xl text-lg flex justify-between items-center"
        >
          <span>{{ todo }}</span>
          <div class="flex">
            <Button><img src="/complete.png" class="w-6 mr-2" /></Button>
            <Button><img src="/remove.png" class="w-6" /></Button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

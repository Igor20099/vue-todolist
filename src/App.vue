<script setup>
import { ref, computed } from "vue";
import NotificationComponent from "./components/NotificationComponent.vue";

const inputTodo = ref("");
const isCompletedTodoList = ref(false);
const todoList = ref([]);
const completeTodoList = ref([]);
const isAdded = ref(false);
const isCompleted = ref(false);
const isRemoved = ref(false);
const inputSearchTodo = ref("");

const addTodo = (todo) => {
  todoList.value.push(todo);
  inputTodo.value = "";
  isAdded.value = true;
  setTimeout(() => (isAdded.value = false), 1000);
};

const removeTodo = (index) => {
  todoList.value.splice(index, 1);
  isRemoved.value = true;
  setTimeout(() => (isRemoved.value = false), 1000);
};

const addTodoInCompleteList = (index) => {
  completeTodoList.value.unshift(todoList.value[index]);
  todoList.value.splice(index, 1);
  isCompleted.value = true;
  setTimeout(() => (isCompleted.value = false), 1000);
};

const searchTodo = computed(() => {
  return todoList.value.filter((todo) => todo.includes(inputSearchTodo.value));
});
const searchCompleteTodo = computed(() => {
  return completeTodoList.value.filter((todo) =>
    todo.includes(inputSearchTodo.value)
  );
});
</script>

<template>
  <div class="w-2/5 m-auto flex flex-col">
    <NotificationComponent :isShowNotif="isAdded">
      <p>Задача добавлена!</p>
    </NotificationComponent>
    <NotificationComponent :isShowNotif="isRemoved">
      <p>Задача удалена!</p>
    </NotificationComponent>
    <NotificationComponent :isShowNotif="isCompleted">
      <p>Задача выполнена!</p>
    </NotificationComponent>
    <h1 class="text-center text-6xl font-bold mb-6 uppercase mt-8">
      Список Задач
    </h1>
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
          @click.prevent="addTodo(inputTodo)"
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

    <div class="flex justify-center mb-8">
      <button
        :class="
          isCompletedTodoList
            ? 'w-1/4 border px-2 py-2 bg-white text-lime-500 transition disabled:bg-slate-300 hover:bg-lime-500 hover:text-white'
            : 'w-1/4 border  px-2 py-2 bg-lime-500 text-white transition disabled:bg-slate-300 '
        "
        @click.prevent="isCompletedTodoList = false"
      >
        Текущие
      </button>
      <button
        :class="
          isCompletedTodoList
            ? 'w-1/4 border px-2 py-2 bg-lime-500 text-white transition disabled:bg-slate-300 mr-4'
            : 'w-1/4 border px-2 py-2 bg-white text-lime-500 transition disabled:bg-slate-300 mr-4 hover:bg-lime-500 hover:text-white'
        "
        @click.prevent="isCompletedTodoList = true"
      >
        Выполненые
      </button>
    </div>
    <div>
      <input
        type="text"
        placeholder="Поиск задачи...."
        class="mr-2 border outline-none rounded-md px-2 py-2 w-full mb-4"
        v-model="inputSearchTodo"
      />
    </div>
    <div>
      <ul class="flex flex-col" v-if="!isCompletedTodoList">
        <li
          v-for="(todo, i) in searchTodo"
          :key="i"
          class="border border-lime-500 p-4 mb-2 rounded-xl text-lg flex justify-between items-center text-lime-500"
        >
          <span>{{ todo }}</span>
          <div class="flex">
            <Button @click.prevent="addTodoInCompleteList(i)"
              ><img src="/complete.png" class="w-6 mr-2"
            /></Button>
            <Button @click.prevent="removeTodo(i)"
              ><img src="/remove.png" class="w-6"
            /></Button>
          </div>
        </li>
      </ul>
      <ul class="flex flex-col" v-else>
        <li
          :key="i"
          v-for="(todo, i) in searchCompleteTodo"
          class="border border-lime-500 p-4 mb-2 rounded-xl text-lg flex justify-center items-center bg-lime-500 text-white"
        >
          <span>{{ todo }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

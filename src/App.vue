<script setup>
import { ref, computed } from "vue";
import NotificationsComponent from "./components/NotificationsComponent.vue";
import FormComponent from "./components/FormComponent.vue";
import TabsComponent from "./components/TabsComponent.vue";
import TodoListComponent from "./components/TodoListComponent.vue";
import { v4 as uuidv4 } from "uuid";

const todoList = ref([]);
const completeTodoList = ref([]);
const isAdded = ref(false);
const isCompleted = ref(false);
const isRemoved = ref(false);
const inputSearchTodo = ref("");
const isCompletedTodoList = ref(false);
const searchQuery = ref("");

const changeList = (isCompleteList) => {
  isCompletedTodoList.value = isCompleteList;
  console.log(isCompletedTodoList.value);
};

const addTodo = (todoText) => {
  const todo = { id: uuidv4(), text: todoText };
  todoList.value.push(todo);
  isAdded.value = true;
  setTimeout(() => (isAdded.value = false), 1000);
};

const removeTodo = (id) => {
  todoList.value = todoList.value.filter((item) => item.id !== id);
  isRemoved.value = true;
  setTimeout(() => (isRemoved.value = false), 1000);
};

const addTodoInCompleteList = (id) => {
  completeTodoList.value.unshift(todoList.value.find((item) => item.id === id));
  todoList.value = todoList.value.filter((item) => item.id !== id);
  isCompleted.value = true;
  setTimeout(() => (isCompleted.value = false), 1000);
};

const searchTodo = computed(() => {
  console.log(searchQuery);
  return todoList.value.filter((todo) => todo.text.includes(searchQuery.value));
});
const searchCompleteTodo = computed(() => {
  return completeTodoList.value.filter((todo) =>
    todo.text.includes(searchQuery.value)
  );
});
</script>

<template>
  <NotificationsComponent
    :isAdded="isAdded"
    :isCompleted="isCompleted"
    :isRemoved="isRemoved"
  />
  <div class="w-2/5 m-auto flex flex-col">
    <h1 class="text-center text-6xl font-bold mb-6 uppercase mt-8">
      Список Задач
    </h1>
    <FormComponent @addTodo="addTodo" />
    <TabsComponent
      @changeList="changeList"
      :isCompletedTodoList="isCompletedTodoList"
    />
    <div>
      <input
        type="text"
        placeholder="Поиск задачи...."
        class="mr-2 border outline-none rounded-md px-2 py-2 w-full mb-4"
        v-model="searchQuery"
      />
    </div>
    <TodoListComponent
      :todoList="searchTodo"
      :completeTodoList="searchCompleteTodo"
      :removeTodo="removeTodo"
      :addTodoInCompleteList="addTodoInCompleteList"
      :isCompletedTodoList="isCompletedTodoList"
    />
  </div>
</template>

<script setup>
import TodoItemComponent from "./TodoItemComponent.vue";
defineProps({
  todoList: Array,
  completeTodoList: Array,
  removeTodo: Function,
  addTodoInCompleteList: Function,
  isCompletedTodoList: Boolean,
});
</script>

<template>
  <div>
    <ul class="flex flex-col" v-if="!isCompletedTodoList">
      <TodoItemComponent
        v-for="todo in todoList"
        :key="todo.id"
        :todo="todo"
        @removeTodo="removeTodo"
        @addTodoInCompleteList="addTodoInCompleteList"
        :isCompletedTodoList="isCompletedTodoList"
        :id="todo.id"
      />
    </ul>
    <ul class="flex flex-col" v-else>
      <TodoItemComponent
        v-for="todo in completeTodoList"
        :key="todo.id"
        :todo="todo"
        :isCompletedTodoList="isCompletedTodoList"
      />
    </ul>
  </div>
</template>

<script setup>
import NotificationComponent from "./NotificationComponent.vue";
defineProps({
  isAdded: Boolean,
  isRemoved: Boolean,
  isCompleted: Boolean,
});
</script>

<template>
  <NotificationComponent :isShowNotif="isAdded">
    <p>Задача добавлена!</p>
  </NotificationComponent>
  <NotificationComponent :isShowNotif="isRemoved">
    <p>Задача удалена!</p>
  </NotificationComponent>
  <NotificationComponent :isShowNotif="isCompleted">
    <p>Задача выполнена!</p>
  </NotificationComponent>
</template>

<script setup>
defineProps({
  isShowNotif: Boolean,
});
</script>

<template>
  <transition name="fade">
    <div
      v-show="isShowNotif"
      class="fixed border border-lime-500 px-20 text-xl py-4 rounded-2xl text-white bg-lime-500 center bottom-7 left-1/3 ml-16 shadow-2xl"
    >
      <slot></slot>
    </div>
  </transition>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

<script setup lang="ts">
import { ref, computed, watch } from 'vue';
import type { AlertProps } from '@/models/alert-props.interface.ts';

const props = withDefaults(defineProps<AlertProps>(), {
  message: 'Tot bé',
  type: 'info',
  duration: 0,
  flag: false,
});
const emit = defineEmits<{ (e: 'alert-visible'): void }>();

const isVisible = ref<boolean>(false);
const style = computed<string>(getStyle);
watch(props, activateMessage);

function activateMessage() {
  if (props.duration <= 0) return;
  isVisible.value = true;
  setTimeout(() => {
    isVisible.value = false;
    emit('alert-visible');
  }, props.duration);
}

function getStyle() {
  switch (props.type) {
    case 'success':
      return 'msg-green';
    case 'warning':
      return 'msg-yellow';
    case 'error':
      return 'msg-red';
    default:
      return '';
  }
}
</script>

<template>
  <main class="container">
    <div v-show="isVisible" class="msg" :class="[style]">
      <div>{{ props.message }}</div>
    </div>
  </main>
</template>

<style scoped>
.msg {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  font-size: 14px;
  color: gray;
  background: lightgray;
  /*border: 1px solid black;*/
}
.msg-green {
  color: green;
  background-color: lightgreen;
}
.msg-yellow {
  color: orangered;
  background-color: lightgoldenrodyellow;
}
.msg-red {
  color: red;
  background-color: lightsalmon;
}
</style>

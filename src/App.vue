<script setup lang="ts">
import { ref } from 'vue';
import AlertComponent from './components/AlertComponent.vue';
import type { AlertProps } from './models/alert-props.interface';

const alertSuccess: AlertProps = {
  message: '✅ OK: Operació correcta',
  type: 'success',
  duration: 3000,
  flag: true,
};
const alertWarning: AlertProps = {
  message: "⚠ WARNING: Missatge d'alerta",
  type: 'warning',
  duration: 3000,
  flag: true,
};
const alertError: AlertProps = {
  message: "❌ ERROR: Missatge d'error",
  type: 'error',
  duration: 3000,
  flag: true,
};
const alertDefault: AlertProps = {
  message: '',
  type: 'info',
  duration: 0,
  flag: true,
};
const isVisible = ref<boolean>(false);
const alert = ref<AlertProps>(alertDefault);

function sendAlert(alertObject: AlertProps): void {
  isVisible.value = true;
  alertObject.flag = !alertObject.flag; //canviem el flag per que l'objecte (props) sigui diferent de l'anterior.
  alert.value = alertObject;
}
</script>

<template>
  <main class="container">
    <h2 class="title" v-once>Component reusable</h2>
    <div class="btn-group" v-once>
      <button
        class="btn btn-green"
        @click="
          isVisible = true;
          sendAlert(alertSuccess);
        "
      >
        Correcte
      </button>
      <button class="btn btn-yellow" @click="sendAlert(alertWarning)">Avís</button>
      <button class="btn btn-red" @click="sendAlert(alertError)">Error</button>
    </div>
    <AlertComponent v-show="isVisible" v-bind="alert" @alert-visible="isVisible = false" />
  </main>
</template>

<style scoped>
.btn-green {
  background: green;
}
.btn-yellow {
  background: yellow;
}
.btn-red {
  background: red;
}
.btn-green:active {
  background-color: lightgreen;
}
.btn-yellow:active {
  background-color: lightyellow;
}
.btn-red:active {
  background-color: lightcoral;
}
.btn-group {
  display: flex;
  justify-content: center;
  gap: 1rem;
  align-items: center;
}
.title {
  display: flex;
  justify-content: center;
}
</style>

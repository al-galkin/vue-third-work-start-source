<template>
  <demo-button @click="show = !show">Показать</demo-button>
  <br>
  <transition
      @before-enter="onBeforeEnter"
      @enter="onEnter"
      @after-enter="onAfterEnter"
      @enter-cancelled="onEnterCancelled"
      @before-leave="onBeforeLeave"
      @leave="onLeave"
      @after-leave="onAfterLeave"
      @leave-cancelled="onLeaveCancelled"
      :css="false"
  >
    <img v-if="show" src="/assets/img/arrow-right.svg" alt="img">
  </transition>
</template>
<script setup>
import DemoButton from "../components/DemoButton.vue";
import { ref } from 'vue'

const show = ref(true)

function clearAnimations (el, done) {
  el.addEventListener('animationend', () => {
    el.className = ''
    done()
  })
}

function onBeforeEnter (el) {}

function onEnter (el, done) {
  // Этот хук должен вызвать метод done
  done()
  el.className = 'bounce'
  clearAnimations(el, done)
}

function onAfterEnter (el) {}

function onEnterCancelled (el) {}

function onBeforeLeave (el) {}

function onLeave (el, done) {
  // Этот хук должен вызвать метод done
  done()
  el.className = 'bounce-reverse'
  clearAnimations(el, done)
}

function onAfterLeave (el) {}

// Будет работать только с директивой v-show
function onLeaveCancelled (el) {}
</script>

<style scoped>
.bounce {
  animation: bounce .5s;
}

.bounce-reverse {
  animation: bounce .5s reverse;
}

@keyframes bounce {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>

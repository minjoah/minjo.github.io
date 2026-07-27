<template>
  <Transition name="welcome">
    <div
      v-if="showWelcome"
      class="welcome-overlay"
    >
     <div class="typing-demo">
        {{ text }}
      </div>
    </div>
  </Transition>
</template>
<script setup>
import { ref, onMounted, nextTick } from 'vue'

const showWelcome = ref(true)
const text = 'comming soon!'

onMounted(async() => {
  await document.fonts.load('32px InkLiquid');
})
</script>
<style scoped lang="scss">
.welcome-overlay {
  position: absolute;
  inset: 0;

  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  align-items: center;

  background: rgba(0, 0, 0, 0.7);
    // border-radius: 25px 25px 0 0 ;
  z-index: 100;
}


.typing-demo {
  display: flex;
  align-items: center;

  white-space: nowrap;

  font-family: 'InkLiquid';
  font-size: 2em;
  font-weight: 300;

  color: var(--section1);

  letter-spacing: 2px;
}

.welcome-leave-active {
  transition: opacity 1.2s ease;
}

.welcome-leave-to {
  opacity: 0;
}
</style>
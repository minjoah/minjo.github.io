<template>
  <Transition name="welcome">
    <div
      v-if="showWelcome"
      class="welcome-overlay"
    >
     <div class="typing-demo">
        {{ displayText }}
        <span
          v-if="showCursor"
          class="cursor"
        />
      </div>
    </div>
  </Transition>
</template>
<script setup>
import { ref, onMounted } from 'vue'

const showWelcome = ref(true)
const showCursor = ref(true)

const displayText = ref('')
const text = '소중한 분들을 초대합니다'

const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms))
}

const startTyping = async () => {
  // 처음 잠깐 대기
  await sleep(700)

  for (const char of text) {
    displayText.value += char

    // 띄어쓰기에서는 살짝 쉬기
    if (char === ' ') {
      await sleep(300)
      continue
    }

    // 글자마다 타이핑 속도를 조금 다르게
    const typingSpeed =
      Math.random() * 100 + 50

    await sleep(typingSpeed)
  }

  // 작성 완료 후 커서 깜빡임
  await sleep(1200)

  showCursor.value = false

  // 화면 유지
  await sleep(500)

  showWelcome.value = false
}

onMounted(() => {
  startTyping()
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
    border-radius: 25px 25px 0 0 ;
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

.cursor {
  width: 2px;
  height: 1.2em;

  margin-left: 4px;

  background: azure;

  animation: blink 0.7s infinite;
}

@keyframes blink {
  0%,
  50% {
    opacity: 1;
  }

  51%,
  100% {
    opacity: 0;
  }
}

.welcome-leave-active {
  transition: opacity 1.2s ease;
}

.welcome-leave-to {
  opacity: 0;
}
</style>
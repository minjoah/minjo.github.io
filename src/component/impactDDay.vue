<template>
  <div ref="impactRef" :class="['impact', { showImpact: isShow }]">
    <div class="text">
      <div class="line">
        <span
          v-for="(char, i) in 'Oct. 31'"
          :key="i"
          :style="{ transitionDelay: isShow ? `${i * 120}ms` : '0ms' }"
        >
          {{ char === " " ? "\u00A0" : char }}
        </span>
      </div>

      <div class="line">
        <span
          v-for="(char, i) in '2026'"
          :key="i"
          :style="{ transitionDelay: isShow ? `${500 + i * 120}ms` : '0ms' }"
        >
          {{ char }}
        </span>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";

const impactRef = ref(null);
const isShow = ref(false);

let observer;

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        requestAnimationFrame(() => {
          isShow.value = true;
        });
      } else {
        isShow.value = false;
      }
    },
    {
      threshold: 0.3,
    },
  );

  observer.observe(impactRef.value);
});

onBeforeUnmount(() => {
  observer.disconnect();
});
</script>
<style lang="scss" scoped>
.impact {
  width: 100%;
  height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;

  background: white;
  transition: background-color 1.2s ease;
}

.impact.showImpact {
  background: var(--accent-color);
}

.text {
  text-align: center;
  font-size: 80px;
  font-family: "Dancing Script", cursive;
  line-height: 1.5;
  color: rgb(244, 244, 244);
}

.line {
  overflow: hidden;
}

.line span {
  display: inline-block;

  opacity: 0;
  transform: translateY(60px);

  transition:
    transform 0.3s cubic-bezier(0.22, 1, 0.36, 1),
    opacity 0.7s ease;
}

.showImpact .line span {
  opacity: 1;
  transform: translateY(0);
}
</style>

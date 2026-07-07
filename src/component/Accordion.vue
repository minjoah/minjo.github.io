<template>
  <div class="accordion">
    <button class="accordion-header" @click="toggle">
      <span>{{ title }}</span>

      <svg
        class="arrow"
        :class="{ open: isOpen }"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
      >
        <path
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          d="M6 9l6 6l6-6"
        />
      </svg>
    </button>

    <Transition
      name="accordion"
      @enter="enter"
      @leave="leave"
      @after-enter="afterEnter"
    >
      <div v-show="isOpen" class="accordion-body">
        <slot />
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  title: {
    type: String,
    default: "",
  },
  defaultOpen: {
    type: Boolean,
    default: false,
  },
});

const isOpen = ref(props.defaultOpen);

const toggle = () => {
  isOpen.value = !isOpen.value;
};

const enter = (el) => {
  el.style.height = "0";
  requestAnimationFrame(() => {
    el.style.height = `${el.scrollHeight}px`;
  });
};

const leave = (el) => {
  el.style.height = `${el.scrollHeight}px`;
  requestAnimationFrame(() => {
    el.style.height = "0";
  });
};

const afterEnter = (el) => {
  el.style.height = "auto";
};
</script>

<style scoped>
.accordion {
  border-radius: 12px;
  /* overflow: hidden; */
  /* background: #f5f2ef; */
}

.accordion-header {
  width: 100%;
  height: 60px;
  padding: 0 20px;

  display: flex;
  align-items: center;
  justify-content: space-between;

  background: white;
  border: 0;
  cursor: pointer;
  border-radius: 15px;
}

.arrow {
  width: 18px;
  height: 18px;
  transition: transform 0.3s;
}

.arrow.open {
  transform: rotate(180deg);
}

.accordion-body {
  z-index: 999;
  padding: 16px;
  background: #f4efeb;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.accordion-enter-active,
.accordion-leave-active {
  transition: all 0.3s ease;
}

.accordion-enter-from,
.accordion-leave-to {
  opacity: 0;
}
</style>

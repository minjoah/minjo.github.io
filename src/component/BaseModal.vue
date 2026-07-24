<template>
  <Teleport to="body">
    <Transition name="modal">
      <div v-if="modelValue" class="modal-overlay" @click="close">
        <div class="modal-content" :class="size" @click.stop>
          <div class="modal-header">
            <slot name="title" />
            <button class="close-btn" @click="close">✕</button>
          </div>

          <div class="modal-body">
            <slot />
          </div>

          <div v-if="$slots.footer" class="modal-footer">
            <slot name="footer" />
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
  closeOnOverlay: {
    type: Boolean,
    default: true,
  },
  size: {
    type: String,
    default: "normal",
  },
});

const emit = defineEmits(["update:modelValue", "close"]);

const close = () => {
  if (!props.closeOnOverlay) return;

  emit("update:modelValue", false);
  emit("close");
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 9999;

  display: flex;
  justify-content: center;
  align-items: center;

  background: rgba(0, 0, 0, 0.5);
}

.modal-content {
  background: white;
  /* border-radius: 12px; */
  overflow: hidden;
}

.normal {
  width: 90%;
  max-width: 500px;
}

.full {
  width: calc(100vw - 32px);
  max-width: 480px;
  height: calc(100dvh - 32px);

  display: flex;
  flex-direction: column;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  padding: 16px 20px;
  border-bottom: 1px solid #eee;
}

.modal-body {
  flex: 1;
  padding: 0;
  overflow: hidden;
}

.modal-footer {
  padding: 16px 20px;
  border-top: 1px solid #eee;
}

.close-btn {
  border: none;
  background: none;
  font-size: 18px;
  cursor: pointer;
  justify-content: flex-end;
  margin-left: auto;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.25s;
}

.modal-enter-active .modal-content,
.modal-leave-active .modal-content {
  transition: transform 0.25s;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-content,
.modal-leave-to .modal-content {
  transform: translateY(20px);
}
</style>

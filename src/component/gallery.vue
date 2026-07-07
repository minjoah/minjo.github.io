<template>
  <div class="gallery">
    <Title title="GALLERY">
      <br />
      <div style="color: #1b1a1a">
        사진을 클릭하시면 전체화면 보기가 가능합니다.
      </div>
    </Title>
    <div
      ref="containerRef"
      class="container"
      :style="{ '--cols': gridCols, height: contentHeight }"
      :class="{ expanded: isExpanded }"
    >
      <div
        class="images"
        v-for="(cols, index) in imageList"
        :key="index"
        @click="showModal = true"
      >
        <img v-for="image in cols" :src="image" />
      </div>
    </div>
    <div v-if="showMoreButton" @click="toggleExpand" class="scroll-more">
      <div v-if="!isExpanded">
        사진 더 보기
        <!-- 열기 아이콘 -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 16 16"
          class="animate"
        >
          <path
            fill="none"
            stroke="currentColor"
            stroke-linejoin="round"
            d="m4 6.5 4 4 4-4"
          />
        </svg>
      </div>
      <div v-else>
        사진 접기
        <!-- 닫기 아이콘 -->
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          class="animate"
        >
          <path
            fill="none"
            stroke="currentColor"
            stroke-linejoin="round"
            d="m4 13 6-6 6 6"
          />
        </svg>
      </div>
    </div>
  </div>

  <BaseModal v-model="showModal" size="full">
    <div class="image-viewer">
      <button class="nav prev" @click="prev">‹</button>
      <div class="image-wrapper">
        <img :src="Object.values(modules)[currentIndex]" class="viewer-image" />
      </div>
      <button class="nav next" @click="next">›</button>
      <div class="pagination">
        {{ currentIndex + 1 }} / {{ Object.values(modules).length }}
      </div>
    </div>
  </BaseModal>
</template>

<script setup>
import { ref, computed, onMounted, watch, nextTick } from "vue";
import Title from "@/component/Title.vue";
import BaseModal from "@/component/BaseModal.vue";
const gridCols = ref(3);
// 더보기 버튼관련
const isExpanded = ref(false);
const containerRef = ref(null);
const showMoreButton = ref(false);
const contentHeight = ref("400px");

const showModal = ref(false);
const toggleExpand = async () => {
  if (!containerRef.value) return;

  if (isExpanded.value) {
    contentHeight.value = `${containerRef.value.scrollHeight}px`;

    await nextTick();

    requestAnimationFrame(() => {
      contentHeight.value = "400px";
      isExpanded.value = false;
    });
  } else {
    contentHeight.value = `${containerRef.value.scrollHeight}px`;
    isExpanded.value = true;
  }
};

const imageList = computed(() => {
  return chunkArray(Object.values(modules), gridCols.value);
});

const modules = import.meta.glob("@/image/gallery/*.jpg", {
  eager: true,
  import: "default",
});
const chunkArray = (arr, n) => {
  const result = [];
  for (let i = 0; i < arr.length; i += n) {
    result.push(arr.slice(i, i + n)); // i부터 i+n까지 잘라서 추가
  }
  return result;
};

const checkHeight = () => {
  if (!containerRef.value) return;

  console.log(containerRef.value.scrollHeight);
  showMoreButton.value = containerRef.value.scrollHeight > 700;
};

//modal
const currentIndex = ref(0);
const prev = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  } else {
    currentIndex.value = Object.values(modules).length - 1;
  }
};

const next = () => {
  if (currentIndex.value < Object.values(modules).length - 1) {
    currentIndex.value++;
  } else {
    currentIndex.value = 0;
  }
};

onMounted(checkHeight);

watch([imageList, gridCols], async () => {
  await nextTick();
  checkHeight();
});
</script>
<style lang="scss" scoped>
.container {
  position: relative; // 추가
  width: 80%;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(var(--cols), 1fr);
  gap: 5px;

  overflow: hidden;
  height: 400px;
  transition: height 0.4s ease;
}

.gallery {
  margin: 100px 0px;
  position: relative;
}

.more-btn {
  display: block;
  margin: 20px auto 0;
}

.container.expanded {
  max-height: 5000px; /* 충분히 큰 값 */
}

.container.expanded::after {
  display: none;
}

.container:not(.expanded)::after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 120px;
  background: linear-gradient(transparent, rgba(255, 255, 255, 0.95));
}

.images {
  display: flex;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
}

.images img {
  width: 100%;
  aspect-ratio: 1;
  object-fit: cover;
  display: block;
}

.scroll-more {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  font-size: 14px;
  color: #959595;
  padding-block: 20px;
  margin-top: 24px;
}

.animate {
  animation: scrollGuide 1.2s ease-in-out infinite;

  vertical-align: middle;
  --icon-size: 1.25rem;
  width: 1.25rem;
}

@keyframes scrollGuide {
  0% {
    transform: translateY(-2px);
    opacity: 1;
  }

  50% {
    transform: translateY(0px);
    // opacity: 0.6;
  }

  100% {
    transform: translateY(-2px);
    opacity: 1;
  }
}

.image-viewer {
  position: relative;
  width: 100%;
  height: 100%;
}

.viewer-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.viewer-image {
  max-width: 100%;
  max-height: 100%;

  width: auto;
  height: auto;

  object-fit: contain;
}
.nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);

  z-index: 10;

  width: 48px;
  height: 48px;

  border: none;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.5);
  color: white;

  font-size: 28px;
  cursor: pointer;

  display: flex;
  align-items: center;
  justify-content: center;
}

.prev {
  left: 12px;
}

.next {
  right: 12px;
}

.pagination {
  position: absolute;
  bottom: 20px;
  left: 50%;

  transform: translateX(-50%);

  color: #1b1a1a;
  font-size: 14px;
}
</style>

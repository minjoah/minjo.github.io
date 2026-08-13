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
      :style="{ height: contentHeight }"
      :class="{ expanded: isExpanded }"
    >
      <div
        v-for="(image, index) in imageList"
        :key="index"
        class="images"
        @click="()=>{
          currentIndex = index
          showModal = true}"
      >
        <img :src="image" />
      </div>
    </div>
    <div v-if="showMoreButton" @click="toggleExpand" class="scroll-more">
      <div v-if="!isExpanded" style="cursor: pointer;">
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
      <div v-else style="cursor: pointer;">
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
        <img :src="imageList[currentIndex]" class="viewer-image" />
      </div>
      <button class="nav next" @click="next">›</button>
      <div class="pagination">
        {{ currentIndex + 1 }} / {{ imageList.length }}
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

  if (!isExpanded.value) {
    const height = getContentHeight();

    contentHeight.value = `${height}px`;
    isExpanded.value = true;
  } else {
    contentHeight.value = `${containerRef.value.offsetHeight}px`;

    requestAnimationFrame(() => {
      contentHeight.value = "400px";
      isExpanded.value = false;
    });
  }
};

const getContentHeight = () => {
  if (!containerRef.value) return 0;

  const containerWidth = containerRef.value.clientWidth;
  const gap = 5;
  const cols = 3;

  const imageWidth =
    (containerWidth - gap * (cols - 1)) / cols;

  const rows = Math.ceil(imageList.value.length / cols);

  return rows * imageWidth + (rows - 1) * gap;
};

const modules = import.meta.glob("@/image/gallery/*.jpg", {
  eager: true,
  import: "default",
});

const imageList = computed(()=>{
  let data = Object.values(modules)
  // data = data.map(i=> i=`/wedding${i}`)
return data.sort()
})

const checkHeight = () => {
  if (!containerRef.value) return;
  showMoreButton.value = containerRef.value.scrollHeight > 700;
};

//modal
const currentIndex = ref(0);
const prev = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  } else {
    currentIndex.value = imageList.value.length - 1;
  }
};

const next = () => {
  if (currentIndex.value < imageList.value.length - 1) {
    currentIndex.value++;
  } else {
    currentIndex.value = 0;
  }
};

onMounted(checkHeight);
</script>
<style lang="scss" scoped>
.container {
  position: relative;
  width: 80%;
  margin: 0 auto;

  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 5px;

  overflow: hidden;
  height: 400px;
  transition: height 0.4s ease;
}

.images {
  cursor: pointer;
}

.images img {
  width: 100%;
  aspect-ratio: 1;
  object-fit: cover;
  display: block;
}
.gallery {
  margin-top: 100px;
  position: relative;
}

.more-btn {
  display: block;
  margin: 20px auto 0;
}

// .container.expanded {
//   max-height: 5000px; /* 충분히 큰 값 */
// }

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


.scroll-more {
   display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  font-size: 14px;
  color: #959595;

  padding-block: 12px;
  margin-top: 0;
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

  display: flex;
  align-items: center;
  justify-content: center;
}

.image-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.viewer-image {
  width: 100%;
  height: auto;
  display: block;
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

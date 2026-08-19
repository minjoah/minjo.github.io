<template>
  <div class="gallery">
    <Title title="GALLERY">
      <br />

      <div style="color: #1b1a1a">
        사진을 클릭하시면 전체화면 보기가 가능합니다.
      </div>
    </Title>

    <!-- 갤러리 -->
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
        @click="openImage(index)"
      >
        <img :src="image" />
      </div>
    </div>

    <!-- 더보기 / 접기 -->
    <div
      v-if="showMoreButton"
      class="scroll-more"
      @click="toggleExpand"
    >
      <div v-if="!isExpanded" style="cursor: pointer">
        사진 더 보기

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

      <div v-else style="cursor: pointer">
        사진 접기

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

  <!-- 전체화면 이미지 모달 -->
  <BaseModal v-model="showModal" size="full">
    <div class="image-viewer">

      <!-- 이미지 영역 -->
      <div class="image-wrapper">
    <Swiper
      class="gallery-swiper"
        :modules="[Zoom]"
          :slides-per-view="1"
            :space-between="0"
              :loop="true"
                :allow-touch-move="true"
                  :zoom="true"
                    :speed="300"
                      @swiper="onSwiper"
                        @slide-change="onSlideChange"
                        >
    
          <SwiperSlide
            v-for="(image, index) in imageList"
              :key="index"
                class="gallery-slide"
                >
                  <div class="swiper-zoom-container">
                      <img
                            :src="image"
                                  class="viewer-image"
                                        draggable="false"
                                            />
                                              </div>
                                              </SwiperSlide>
        </Swiper>
      </div>

      <!-- 하단 컨트롤 -->
      <div class="viewer-controls">

        <!-- 이전 -->
        <button
          type="button"
          class="nav prev"
          aria-label="이전 사진"
          @click="prev"
        >
          ‹
        </button>

        <!-- 페이지 번호 -->
        <div class="pagination">
          {{ currentIndex + 1 }} / {{ imageList.length }}
        </div>

        <!-- 다음 -->
        <button
          type="button"
          class="nav next"
          aria-label="다음 사진"
          @click="next"
        >
          ›
        </button>

      </div>
    </div>
  </BaseModal>
</template>

<script setup>
import {
  ref,
  computed,
  onMounted,
  nextTick,
  watch,
  onBeforeUnmount,
} from "vue";

import Title from "@/component/Title.vue";
import BaseModal from "@/component/BaseModal.vue";

import { Swiper, SwiperSlide } from "swiper/vue";
import { Zoom } from "swiper/modules";

import "swiper/css";
import "swiper/css/zoom";

/* ==================================================
   Gallery Image
================================================== */

const modules = import.meta.glob(
  "@/image/gallery/*.jpg",
  {
    eager: true,
    import: "default",
  }
);

const imageList = computed(() => {
  const data = Object.values(modules);

  return data.sort();
});

/* ==================================================
   Gallery More / Collapse
================================================== */

const isExpanded = ref(false);

const containerRef = ref(null);

const showMoreButton = ref(false);

const contentHeight = ref("400px");

const toggleExpand = () => {
  if (!containerRef.value) return;

  if (!isExpanded.value) {
    const height = getContentHeight();

    contentHeight.value = `${height}px`;

    isExpanded.value = true;
  } else {
    contentHeight.value =
      `${containerRef.value.offsetHeight}px`;

    requestAnimationFrame(() => {
      contentHeight.value = "400px";

      isExpanded.value = false;
    });
  }
};

const getContentHeight = () => {
  if (!containerRef.value) {
    return 0;
  }

  const containerWidth =
    containerRef.value.clientWidth;

  const gap = 5;

  const cols = 3;

  const imageWidth =
    (containerWidth - gap * (cols - 1)) / cols;

  const rows =
    Math.ceil(imageList.value.length / cols);

  return (
    rows * imageWidth +
    (rows - 1) * gap
  );
};

const checkHeight = () => {
  if (!containerRef.value) return;

  showMoreButton.value =
    containerRef.value.scrollHeight > 700;
};

/* ==================================================
   Modal
================================================== */

const showModal = ref(false);
let scrollY = 0;

const lockBodyScroll = () => {
  scrollY = window.scrollY;

  document.body.style.position = "fixed";
  document.body.style.top = `-${scrollY}px`;
  document.body.style.left = "0";
  document.body.style.right = "0";
  document.body.style.width = "100%";
};

const unlockBodyScroll = () => {
  document.body.style.position = "";
  document.body.style.top = "";
  document.body.style.left = "";
  document.body.style.right = "";
  document.body.style.width = "";

  window.scrollTo(0, scrollY);
};

watch(showModal, (isOpen) => {
  if (isOpen) {
    lockBodyScroll();
  } else {
    unlockBodyScroll();
  }
});

onBeforeUnmount(() => {
  unlockBodyScroll();
});

const currentIndex = ref(0);

/* ==================================================
   Swiper
================================================== */

const swiperRef = ref(null);

/**
 * 갤러리 이미지 클릭
 */
const openImage = async (index) => {
  currentIndex.value = index;

  showModal.value = true;

  await nextTick();

  if (swiperRef.value) {
    swiperRef.value.slideToLoop(
      index,
      0
    );
  }
};

/**
 * Swiper 인스턴스
 */
const onSwiper = (swiper) => {
  swiperRef.value = swiper;

  swiper.slideToLoop(
    currentIndex.value,
    0
  );
};

/**
 * 현재 이미지 변경
 */
const onSlideChange = (swiper) => {
  currentIndex.value =
    swiper.realIndex;
};

/**
 * 이전 이미지
 */
const prev = () => {
  if (!swiperRef.value) return;

  swiperRef.value.slidePrev();
};

/**
 * 다음 이미지
 */
const next = () => {
  if (!swiperRef.value) return;

  swiperRef.value.slideNext();
};

/* ==================================================
   Mounted
================================================== */

onMounted(() => {
  checkHeight();
});
</script>

<style lang="scss" scoped>

/* ==================================================
   Gallery
================================================== */

.gallery {
  margin-top: 100px;
  position: relative;
}

/* ==================================================
   Gallery Container
================================================== */

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

/* ==================================================
   Gradient
================================================== */

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

  background:
    linear-gradient(
      transparent,
      rgba(255, 255, 255, 0.95)
    );
}

/* ==================================================
   More Button
================================================== */

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
  animation:
    scrollGuide 1.2s
    ease-in-out infinite;

  vertical-align: middle;

  width: 1.25rem;
}

@keyframes scrollGuide {
  0% {
    transform: translateY(-2px);
    opacity: 1;
  }

  50% {
    transform: translateY(0);
  }

  100% {
    transform: translateY(-2px);
    opacity: 1;
  }
}

/* ==================================================
   Image Viewer
================================================== */

.image-viewer {
  position: relative;

  width: 100%;
  height: 100%;

  display: flex;

  flex-direction: column;

  align-items: center;
  justify-content: center;
}

/* ==================================================
   Image Wrapper
================================================== */

.image-wrapper {
  width: 100%;

  flex: 1;

  min-height: 0;

  display: flex;

  align-items: center;
  justify-content: center;
}

/* ==================================================
   Swiper
================================================== */

.gallery-swiper {
  width: 100%;
  height: 100%;
}

.gallery-slide {
  width: 100%;
  height: 100%;

  display: flex;

  align-items: center;
  justify-content: center;
}

/* ==================================================
   Viewer Image
================================================== */

.viewer-image {
  width: 100%;

  height: auto;

  max-height: 100%;

  display: block;

  object-fit: contain;

  user-select: none;

  -webkit-user-drag: none;
}

/* ==================================================
   Bottom Controls
================================================== */

.viewer-controls {
  position: relative;

  width: 100%;

  flex-shrink: 0;

  display: flex;

  align-items: center;
  justify-content: center;

  padding: 12px 20px 20px;

  box-sizing: border-box;
}

/* ==================================================
   Navigation Button
================================================== */

.nav {
  position: absolute;

  top: 50%;

  transform: translateY(-50%);

  width: 36px;
  height: 36px;

  padding: 0;

  border: none;

  background: transparent;

  color: #1b1a1a;

  font-size: 30px;

  line-height: 1;

  cursor: pointer;

  display: flex;

  align-items: center;
  justify-content: center;

  appearance: none;
}

/* 버튼 양끝 배치 */

.nav.prev {
  left: 20px;
}

.nav.next {
  right: 20px;
}

/* ==================================================
   Pagination
================================================== */

.pagination {
  min-width: 60px;

  text-align: center;

  color: #1b1a1a;

  font-size: 14px;
}

/* ==================================================
   Mobile
================================================== */

@media (max-width: 768px) {
  .container {
    width: 90%;
  }

  .image-wrapper {
    width: 100%;
  }

  .gallery-swiper {
    width: 100%;
    height: 100%;
  }

  .gallery-slide {
    width: 100%;
    height: 100%;
  }

  .viewer-image {
    width: 100%;

    max-width: 100%;
    max-height: 100%;

    object-fit: contain;
  }

  .viewer-controls {
    width: 100%;

    padding: 10px 16px 16px;
  }

  .nav {
    width: 34px;
    height: 34px;

    font-size: 28px;

    color: #1b1a1a;
  }

  .nav.prev {
    left: 16px;
  }

  .nav.next {
    right: 16px;
  }

  .pagination {
    min-width: 55px;

    font-size: 13px;

    color: #1b1a1a;
  }
}
</style>
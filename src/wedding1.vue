<template>
  <div
    class="main-frame"
    :class="{
      'font-normal': fontOpt === 'normal',
      'font-large': fontOpt === 'big',
    }"
  >
    <div>
      <a href="https://minjoah.github.io/wedding" target="_blank"
        >사이트 가기
      </a>
    </div>
    <div class="contents">
      <button @click="fontOpt = 'big'">큰글씨</button>
      <button @click="fontOpt = 'normal'">보통글씨</button>
      <br />
      현재 적용 :: {{ fontOpt === "big" ? "큰글씨" : "보통글씨" }}
    </div>
    <div class="contents">오디오</div>
    <div class="contents">
      메인 사진, 시간장소
      <img src="@/image/image1.png" class="image" />
    </div>
    <div class="contents">웰컴 문구</div>
    <div class="contents">신랑신부소개</div>
    <div class="contents margin backColor_1">
      <calendar />
    </div>
    <div class="contents backColor_1" style="padding-bottom: 120px">
      <!-- 디데이 -->
      <dDay />
    </div>
    <div class="contents">
      <gallery />
    </div>
    <div class="contents backColor_1">
      <Title title="LOCATION" />
      <location />
    </div>
    <div class="contents backColor_1 margin">
      <directions />
    </div>
    <div class="contents">버스대절 안내</div>
    <div class="contents">방명록 ( 필요없을듯 )</div>
    <div class="contents margin">
      <money />
    </div>
    <div class="contents">
      공유, 모청주소 복사
      <share />
    </div>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
import calendar from "@/component/calendar.vue";
import dDay from "@/component/dDay.vue";
import gallery from "@/component/gallery.vue";
import location from "@/component/location.vue";
import directions from "@/component/directions.vue";
import money from "@/component/money.vue";
import share from "@/component/share.vue";
import Title from "@/component/Title.vue";

const fontOpt = ref("normal");
onMounted(() => {
  const callback = ([entry], observer) => {
    if (entry.isIntersecting) {
      entry.target.classList.add("show");
    }
  };
  const observer = new IntersectionObserver(callback, null);
  const boxes = document.querySelectorAll(".contents");
  boxes.forEach((box) => {
    observer.observe(box);
  });
});
</script>
<style lang="scss" scoped>
@use "@/common.scss";

.main-frame {
  width: 100%;

  margin: 0 auto;

  background: #fff;

  display: flex;
  flex-direction: column;
}

.image {
  display: block;
  width: 100%;
  max-width: 100%;
  height: auto;
}

@media (max-width: 1400px) {
  .main-frame {
    width: 100%;
  }
}

.contents {
  width: 100%;
  overflow: hidden;

  // border: 1px solid red;
  font-family: "IBM Plex Sans KR", sans-serif;
  font-weight: 400;
  font-style: normal;
  color: rgb(48, 48, 48);
  .image {
    width: 100%;
  }
}

.backColor_1 {
  background-color: rgb(244, 243, 243);
}
.backColor_2 {
  background-color: rgb(234, 232, 232);
}

.contents.show {
  animation: fadein 3s;
}
.margin {
  padding: 0px 10%;
}
@keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>

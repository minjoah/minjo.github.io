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

      https://www.svgrepo.com/collections/line/35
      https://toourguest.com/preview/jeju
    </div>
    <div class="contents">
      <button @click="fontOpt = 'big'">큰글씨</button>
      <button @click="fontOpt = 'normal'">보통글씨</button>
      <br />
      현재 적용 :: {{ fontOpt === "big" ? "큰글씨" : "보통글씨" }}
    </div>
    <div class="contents">
      테마
      <button @click="changeTheme('yellow')">Yellow</button>

      <button @click="changeTheme('rose')">Rose Beige</button>

      <button @click="changeTheme('purple')">Purple</button>

      <button @click="changeTheme('gray')">Gray</button>

      <button @click="changeTheme('brown')">Brown</button>
    </div>
    <div class="contents">오디오</div>
    <div class="contents">
      메인 사진, 시간장소
      <mainImage />
    </div>
    <div class="contents"><invite /></div>
    <div class="contents">
      <img src="@/image/image2.png" class="image" />
    </div>
    <div class="contents">
      <impactDDay />
    </div>
    <div class="contents margin backColor_1">
      <calendar />
    </div>
    <div class="contents backColor_1 margin">
      <!-- 디데이 -->
      <dDay />
    </div>
    <div class="contents backColor_2">
      <gallery />
    </div>
    <div class="contents backColor_3">
      <location />
    </div>
    <div class="contents backColor_3 margin">
      <directions />
    </div>
    <div class="contents">버스대절 안내</div>
    <div class="contents">방명록 ( 필요없을듯 )</div>
    <div class="contents margin backColor_default">
      <money />
    </div>
    <div class="contents">
      <img src="@/image/image3.png" class="image" />
    </div>
    <div class="contents margin backColor_default">
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
import invite from "@/component/invite.vue";
import impactDDay from "@/component/impactDDay.vue";
import mainImage from "@/component/mainImage.vue";

const themes = {
  yellow: {
    bg: "#EADAA9",
    section1: "#F4F3F3",
    section2: "#f7f0d9",
    section3: "#F7F0D9",
    button: "#DAC37F",
    accent: "#B89B4B",
    text: "#3C3C3C",
  },

  rose: {
    bg: "#EFD9DD",
    section3: "#FCF2F4",
    section1: "#F9ECEF",
    section2: "#F3E2E7",
    button: "#D9A7B3",
    accent: "#B87889",
    text: "#534446",
  },

  purple: {
    bg: "#DDD6EA",
    section3: "#F6F3FB",
    section1: "#F0EDF8",
    section2: "#E8E2F3",
    button: "#B7A2D8",
    accent: "#8669B2",
    text: "#433B52",
  },

  gray: {
    bg: "#D9D9D9",
    section3: "#F5F5F5",
    section1: "#F2F2F2",
    section2: "#EBEBEB",
    button: "#A9A9A9",
    accent: "#7A7A7A",
    text: "#3F3F3F",
  },

  brown: {
    bg: "#DCCEBF",
    section3: "#F6F0E8",
    section1: "#F2EBE2",
    section2: "#E9DFD3",
    button: "#B89572",
    accent: "#8D6B4D",
    text: "#463A31",
  },
};

const changeTheme = (name) => {
  const theme = themes[name];

  const root = document.documentElement;

  root.style.setProperty("--bg-color", theme.bg);
  root.style.setProperty("--section1", theme.section1);
  root.style.setProperty("--section2", theme.section2);
  root.style.setProperty("--section3", theme.section3);

  root.style.setProperty("--button-color", theme.button);
  root.style.setProperty("--accent-color", theme.accent);
  root.style.setProperty("--text-color", theme.text);
};

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
  background-color: var(--section1);
}
.backColor_2 {
  background-color: var(--section2);
}
.backColor_3 {
  background-color: var(--section3);
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

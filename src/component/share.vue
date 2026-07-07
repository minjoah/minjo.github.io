<template>
  <div class="button-group">
    <button class="action-button primary" @click="shareMessage()">
      <span>카카오톡으로 청첩장 전하기</span>

      <svg
        class="icon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="none"
      >
        <path
          d="M7 17L17 7M17 7H9M17 7V15"
          stroke="currentColor"
          stroke-width="1.8"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>

    <button class="action-button secondary" @click="copy()">
      <span>청첩장 주소 복사하기</span>

      <svg
        class="icon"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="none"
      >
        <rect
          x="8"
          y="4"
          width="10"
          height="14"
          rx="2"
          stroke="currentColor"
          stroke-width="1.6"
        />
        <rect
          x="5"
          y="7"
          width="10"
          height="14"
          rx="2"
          stroke="currentColor"
          stroke-width="1.6"
        />
      </svg>
    </button>
  </div>

  <Toast :message="toastMessage" :duration="2000" />
</template>

<script setup>
import { ref, watch } from "vue";
import Toast from "@/component/Toast.vue";
const shareMessage = () => {
  Kakao.Share.sendDefault({
    objectType: "feed",
    content: {
      title: "승현민조결혼식",
      // description: "#케익 #딸기 #삼평동 #카페 #분위기 #소개팅",
      imageUrl:
        "http://k.kakaocdn.net/dn/bLPLfX/dJMcacayNt1/iWQpxLOqbqcyg2hxzKCEE1/kakaolink40_original.png",
      link: {
        mobileWebUrl: "https://minjoah.github.io/wedding",
        webUrl: "https://minjoah.github.io/wedding",
      },
    },
    // social: {
    //   likeCount: 286,
    //   commentCount: 45,
    //   sharedCount: 845,
    // },
    buttons: [
      {
        title: "웹으로 보기",
        link: {
          mobileWebUrl: "https://minjoah.github.io/wedding",
          webUrl: "https://minjoah.github.io/wedding",
        },
      },
      {
        title: "앱으로 보기",
        link: {
          mobileWebUrl: "https://minjoah.github.io/wedding",
          webUrl: "https://minjoah.github.io/wedding",
        },
      },
    ],
  });
};

const toastMessage = ref("");
const copy = () => {
  navigator.clipboard
    .writeText("https://minjoah.github.io/wedding/")
    .then(() => {
      console.log("Text copied to clipboard...");
      toastMessage.value = "";
      requestAnimationFrame(() => {
        toastMessage.value = "복사되었습니다.";
      });
    })
    .catch((err) => {
      console.log("Something went wrong", err);
    });
};
</script>
<style lang="scss" scoped>
.button-group {
  display: flex;
  flex-direction: column;
  gap: 12px;

  width: 100%;
  margin: 40px auto;
}

.action-button {
  display: flex;
  align-items: center;
  justify-content: space-between;

  width: 100%;
  height: 48px;

  padding: 0 18px;

  border: none;
  border-radius: 12px;

  cursor: pointer;

  font-size: 15px;
  font-weight: 500;

  transition: all 0.2s ease;
}

.action-button .icon {
  width: 22px;
  height: 22px;
  flex-shrink: 0;
}

.action-button:hover {
  transform: translateY(-1px);
}

.action-button.primary {
  background: var(--button-color);
  color: var(--button-text);
}

.action-button.secondary {
  background: var(--accent-color);
  color: var(--button-text);
}
</style>

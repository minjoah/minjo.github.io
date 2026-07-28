<template>
  <div class="text">
    <b>마음 전하실 곳</b>
    <br />
    <br />
    참석이 어려우신 분들을 위해 기재했습니다 <br />
    너그러운 마음으로 양해 부탁드립니다
  </div>

  <div class="account-accordion">
    <Accordion title="신랑측에게" class="accordion">
      <div
        v-for="account in accounts"
        :key="account.accountNo"
        class="account-card"
      >
        <div class="account-card__header">
          <span>{{ account.role }}</span>
          <span>{{ account.name }}</span>
        </div>

        <div class="account-card__body">
          <div class="account-card__info">
            <div class="account-card__bank">
              {{ account.bank }}
            </div>

            <div class="account-card__number">
              {{ account.accountNo }}
            </div>
          </div>

          <div class="account-card__actions">
             <button class="icon-btn" v-if="account.isKakaoPay">
              <img
                src="@/image/icon/kakaopay.png"
                class="icon_kakao"
                @click="() => goLink(account.kakaoPayLink)"
              />
            </button>
            <button class="icon-btn" @click="copy(account.accountNo)">
              <img src="@/image/icon/copy.svg" class="icon" />
            </button>
           
          </div>
        </div>
      </div>
    </Accordion>
    <Accordion title="신부측에게" class="accordion">
      <div
        v-for="account in accounts1"
        :key="account.accountNo"
        class="account-card"
      >
        <div class="account-card__header">
          <span>{{ account.role }}</span>
          <span>{{ account.name }}</span>
        </div>

        <div class="account-card__body">
          <div class="account-card__info">
            <div class="account-card__bank">
              {{ account.bank }}
            </div>

            <div class="account-card__number">
              {{ account.accountNo }}
            </div>
          </div>

          <div class="account-card__actions">
            <button class="icon-btn" v-if="account.isKakaoPay">
              <img
                src="@/image/icon/kakaopay.png"
                class="icon_kakao"
                @click="() => goLink(account.kakaoPayLink)"
              />
            </button>
            <button class="icon-btn" @click="copy(account.accountNo)">
              <img src="@/image/icon/copy.svg" class="icon" />
            </button>
          
          </div>
        </div>
      </div>
    </Accordion>
  </div>

  <Toast :message="toastMessage" :duration="2000" />
</template>
<script setup>
import { ref, watch } from "vue";
import Accordion from "@/component/Accordion.vue";
import Toast from "@/component/Toast.vue";
const accounts = [
  {
    role: "신랑",
    name: "윤승현",
    bank: "국민은행",
    accountNo: "204402-04-068327",
  },
  {
    role: "신랑 아버지",
    name: "윤춘섭",
    bank: "국민은행",
    accountNo: "204402-04-006268",
  },
  {
    role: "신랑 어머니",
    name: "고순희",
    bank: "국민은행",
    accountNo: "204401-04-028272",
  },
];

const accounts1 = [
  {
    role: "신부",
    name: "김민조",
    bank: "카카오뱅크",
    accountNo: "3333-02-4595352",
    isKakaoPay: true,
    kakaoPayLink: "https://qr.kakaopay.com/Ej7lXpjEN",
  },
  {
    role: "신부 아버지",
    name: "김영일",
    bank: "국민은행",
    accountNo: "1142-10215525",
  },
  {
    role: "신부 어머니",
    name: "이미선",
    bank: "기업은행",
    accountNo: "010-9808-9236",
  },
];

const goLink = (link) => {
  if (!link) return;
  if (!isMobile()) {
    alert("모바일만 지원하는 기능입니다.");
    return;
  }
  window.open(link);
};

const isMobile = () => {
  // 클라이언트 측에서만 navigator 객체를 사용
  return /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
    navigator.userAgent,
  );
};

const toastMessage = ref("");
const copy = (account) => {
  navigator.clipboard
    .writeText(account.replaceAll("-", ""))
    .then(() => {
      console.log("Text copied to clipboard...");
      toastMessage.value = "";
      requestAnimationFrame(() => {
        toastMessage.value = "계좌번호가 복사되었습니다.";
      });
    })
    .catch((err) => {
      console.log("Something went wrong", err);
    });
};
</script>
<style lang="scss" scoped>
.text {
  line-height: 1.8;
}
.account-accordion {
  margin: 50px 0px;
}
.account-card {
  margin: 0;

  border-radius: 16px;
  padding: 20px;

  background: #fff;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
}

.account-card:first-child {
  margin-top: 0;
}

.account-card__header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  margin-bottom: 20px;

  line-height: 1.4;
}

.account-card__body {
  background: #f5f5f5;
  border-radius: 10px;

  padding: 15px 10px;

  display: flex;
  align-items: center;
  justify-content: space-between;
}

.account-card__info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.account-card__bank {
  color: #9a9a9a;
  line-height: 1;
  margin-bottom: 6px;
}

.account-card__number {
  line-height: 1;
}

.account-card__actions {
  display: flex;
  align-items: center;
  gap: 2px;
}

.icon-btn {
  display: flex;
  align-items: center;
  justify-content: center;

  border: 0;
  background: transparent;
  cursor: pointer;

  img {
    width: 18px;
    height: 18px;
  }
}

.icon_kakao {
  width: 45px !important;
  height: 20px !important;
}

.accordion {
  margin-bottom: 15px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
}
</style>

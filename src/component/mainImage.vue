<template>
  <button @click="select = 1">1</button>
  <button @click="select = 2">2</button>
  <button @click="select = 3">3</button>
  <section v-if="select === 1" class="concept1">
    <div class="name top">DOHUN</div>

    <div class="photo-wrap">
      <div class="side left">2027년 10월 16일 토요일 오후 1시</div>

      <div class="photo">
        <img src="@/image/image1.png" class="image" />
      </div>

      <div class="side right">매일 지금처럼 함께 행복하기를</div>
    </div>

    <div class="name bottom">JIYEON</div>
  </section>
  <section v-if="select === 2" class="concept2">
    <div class="photo-wrap">
      <div class="photo">
        <img src="@/image/image1.png" class="image" />
      </div>
    </div>
    <br />
    <div class="name bottom">our wedding day</div>
    <div class="name bottom">2026.10.31 Saturday 15:00</div>
  </section>
  <section v-if="select === 3" class="concept3">
    <div class="name">our wedding day</div>
    <hr />
    <div class="name">2026.10.31 Saturday 15:00</div>
    <div class="name">w웨딩 K웨딩홀</div>
    <br />
    <div class="photo-wrap">
      <div class="photo">
        <img src="@/image/image1.png" class="image" />
      </div>
    </div>
  </section>
</template>
<script setup>
import { ref } from "vue";
const select = ref(1);
</script>
<style lang="scss" scoped>
.concept1 {
  padding: 60px 0 80px;
  background: #f8f8f8;

  display: flex;
  flex-direction: column;
  align-items: center;

  .name {
    font-size: 68px;
    font-family: "Cormorant Garamond", serif;
    font-weight: 300;
    letter-spacing: 4px;
    color: #555;
  }

  .top {
    margin-bottom: 50px;
  }

  .bottom {
    margin-top: 50px;
  }

  .photo-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 20px;
  }

  .side {
    font-size: 14px;
    color: #666;
    letter-spacing: 2px;
    text-orientation: sideways;
  }

  /* 왼쪽 : 아래 → 위 */
  .left {
    writing-mode: vertical-lr;
  }

  /* 오른쪽 : 위 → 아래 */
  .right {
    writing-mode: vertical-rl;
  }
  /* 사진 */

  .photo {
    width: 280px;
    height: 420px;

    overflow: hidden;

    border-radius: 50% / 36%;
  }

  .photo img {
    width: 100%;
    height: 100%;

    object-fit: cover;
  }
}

.concept2 {
  padding: 60px 0 80px;
  background: #f8f8f8;

  display: flex;
  flex-direction: column;
  align-items: center;

  .photo-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 20px;
  }

  .photo {
    width: 360px;
    height: 500px;

    overflow: hidden;

    border-radius: 47% 47% 0% 0%;
  }

  .photo img {
    width: 100%;
    height: 100%;

    object-fit: cover;
  }
}

.concept3 {
  padding: 60px 0 80px;
  background: #f8f8f8;

  display: flex;
  flex-direction: column;
  align-items: center;

  .photo-wrap {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 20px;
  }

  .photo {
    width: 360px;
    height: 500px;

    overflow: hidden;

    border-radius: 5%;
  }

  .photo img {
    width: 100%;
    height: 100%;

    object-fit: cover;
  }
}
</style>

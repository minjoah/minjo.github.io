<template>
  <section class="main_image concept5">
    <div class="photo-wrap">
      <div class="sakura-container">
        <div
          v-for="sakura in sakuras"
          :key="sakura.id"
          class="sakura"
          :style="sakura.style"
        />  
        <!-- JavaScript로 벚꽃잎이 채워집니다 -->
        <div class="photo">
          <div  class="top-text">
            we are getting<br/> Married!
          </div>
          <img src="@/image/image4.jpg" class="image" />
          <div class="bottom-gradient"></div>
          <div  class="bottom-text">
           October 31 &nbsp;&nbsp; | &nbsp;&nbsp;  SATURDAY &nbsp;&nbsp;  | &nbsp;&nbsp;  2026<br/>
           at 03:00 PM
          </div>

        </div>
      </div>
      <!-- <br/>
      <div class="name">신랑 윤승현 ♥ 신부 김민조</div>
      <br/><br/>
      <div class="name">2026.10.31 Saturday 15:00</div>
      <div class="name">w웨딩 K웨딩홀</div>
      <br/>
      <br/><br/> -->
  </div>
   
  </section>
</template>
<script setup>
import {
  ref,
  watch,
  onBeforeUnmount,
  onMounted
} from "vue";

const sakuras = ref([]);

let intervalSakura = null;
let sakuraId = 0;

const createSakura = () => {
  const id = sakuraId++;

  const size = Math.random() * 10 + 7;

  const startX = Math.random() * 40 + 80;
  // 80% ~ 120%

  const startY = Math.random() * 70 - 20;
  // -20% ~ 50%

  // 이동 거리
  const moveX = Math.random() * 300 + 400;
  const moveY = Math.random() * 250 + 100;

  // 좌우 흔들림
  const sway1 = Math.random() * 80 + 20;
  const sway2 = Math.random() * 100 + 30;

  // 7 ~ 12초
  const duration = Math.random() * 5 + 7;

  const sakura = {
    id,

    style: {
      width: `${size}px`,
      height: `${size * 0.7}px`,

      left: `${startX}%`,
      top: `${startY}%`,

      "--move-x": `${moveX}px`,
      "--move-y": `${moveY}px`,

      "--sway-1": `${sway1}px`,
      "--sway-2": `${sway2}px`,

      "--rotate": `${Math.random() * 720 + 360}deg`,

      animationDuration: `${duration}s`,
    },
  };

  sakuras.value.push(sakura);

  setTimeout(() => {
    sakuras.value = sakuras.value.filter(
      item => item.id !== id
    );
  }, duration * 1000);
};

const startSakura = () => {
  stopSakura();

  // 시작할 때 자연스럽게 몇 개 생성
  for (let i = 0; i < 10; i++) {
    setTimeout(createSakura, i * 350);
  }

  intervalSakura = setInterval(() => {
    if (Math.random() > 0.35) {
      createSakura();
    }
  }, 500);
};

const stopSakura = () => {
  if (intervalSakura) {
    clearInterval(intervalSakura);
    intervalSakura = null;
  }

  sakuras.value = [];
};

onMounted(()=>{
  startSakura();
})

onBeforeUnmount(() => {
  stopSakura();
});
</script>
<style lang="scss" scoped>
.main_image {
  height: var(--vh); 
}

.concept5 {
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
    width: 100%;
    height: var(--vh);
    position: relative;
    overflow: hidden;
  }

  .photo .image {
    width: 100%;
    height: var(--vh);

    object-fit: cover;
  }

  
  .bottom-gradient {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 40%; /* 하단에서부터 차지하는 높이 비율 */
    background: linear-gradient(to top, rgba(255, 254, 254, 0.7), transparent);
  }

  .top-text{
    position: absolute;
    top: 3%;
    width:100%;
    height: 20%;
    font-family: "InkLiquid";
    font-size:72px;
    color:#fffff9;
    line-height: 1.1;
    // text-shadow: -2px 0px rgb(37, 37, 37), 0px 1px rgb(14, 14, 14), 1px 0px rgb(10, 10, 10), 0px -1px rgb(3, 3, 3);
    text-shadow: -1px 0px rgb(239, 239, 114), 0px 1px rgb(234, 234, 217), 1px 0px rgb(118, 118, 118), 0px -1px rgb(236, 217, 217);
    // margin:10px
  }
  

  .bottom-text{
    position: absolute;
    bottom: 0;
    width:100%;
    height: 18%;
    font-family: "Edu VIC WA NT Hand";
    font-size:15px;
  }

  .title {
    margin: 30px 0px;
    font-family: "Meddon", cursive;
    font-style: normal;
    font-size: 25px;
  }

  .name {
    font-size: 15px;
    line-height: 1.5;
  }


  .sakura-container {
    position: relative;

    width: 100%;
    height: 100%;

    display: flex;
    justify-content: center;

    overflow: hidden;

    pointer-events: none;
  }

  .sakura {
    position: absolute;

    background: linear-gradient(
      135deg,
      #ffffff,
      #fff2f5
    );
    
    border-radius:
      80% 20% 70% 30% /
      70% 30% 80% 20%;

    opacity: 0;

    z-index: 5;
    pointer-events: none;

    animation-name: sakura-wind;
    animation-timing-function: linear;
    animation-fill-mode: forwards;

    will-change: transform;
  }

 @keyframes sakura-wind {
    0% {
      transform:
        translate(0, 0)
        rotate(0deg)
        rotateY(0deg);

      opacity: 0;
    }

    8% {
      opacity: 0.8;
    }

    20% {
      transform:
        translate(
          calc(var(--move-x) * -0.2 + 8px),
          calc(var(--move-y) * 0.15)
        )
        rotate(70deg)
        rotateY(60deg);
    }

    40% {
      transform:
        translate(
          calc(var(--move-x) * -0.4 - 12px),
          calc(var(--move-y) * 0.35)
        )
        rotate(150deg)
        rotateY(130deg);
    }

    60% {
      transform:
        translate(
          calc(var(--move-x) * -0.6 + 15px),
          calc(var(--move-y) * 0.55)
        )
        rotate(230deg)
        rotateY(220deg);
    }

    80% {
      transform:
        translate(
          calc(var(--move-x) * -0.8 - 8px),
          calc(var(--move-y) * 0.8)
        )
        rotate(320deg)
        rotateY(320deg);

      opacity: 0.7;
    }

    100% {
      transform:
        translate(
          calc(var(--move-x) * -1),
          var(--move-y)
        )
        rotate(var(--rotate))
        rotateY(480deg);

      opacity: 0;
    }
  }
} 
</style>

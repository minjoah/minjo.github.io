<template>
  <!-- <button @click="select = 1">1</button>
  <button @click="select = 2">2</button>
  <button @click="select = 3">3</button>
  <button @click="select = 4">4</button> -->
  <section v-if="select === 1" class="main_image concept1">
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
  <section v-if="select === 2" class="main_image concept2">
    <div class="photo-wrap">
      <div class="photo">
        <img src="@/image/image1.png" class="image" />
      </div>
    </div>
    <br />
    <div class="title bottom">our wedding day</div>
    <div class="name bottom">2026.10.31 Saturday 15:00</div>
  </section>
  <section v-if="select === 3" class="main_image concept3">
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
   <section v-if="select === 4" class="main_image concept4">

    <div class="concept4-body">
    <div class="title">We are getting <br/>married</div>

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
        <img src="@/image/image4.jpg" class="image" />
      </div>
    </div>
  </div>
    <br/>
    <div class="name">신랑 윤승현 ♥ 신부 김민조</div>
    <br/><br/>
    <div class="name">2026.10.31 Saturday 15:00</div>
    <div class="name">w웨딩 K웨딩홀</div>
    <br/>
    <br/><br/>
    </div>
   
  </section>
  <section v-if="select === 5" class="main_image concept5">
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

const select = ref(5);
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

watch(select, value => {
  if (value === 5) {
    startSakura();
  } else {
    stopSakura();
  }
});

onMounted(()=>{
  startSakura();
})

onBeforeUnmount(() => {
  stopSakura();
});
</script>
<style lang="scss" scoped>
.main_image {
  height: 100vh; 
}
.concept1 {
  padding: 60px 0 80px;
  background: #f8f8f8;

  display: flex;
  flex-direction: column;
  align-items: center;

  .name {
    font-size: 68px;
    font-family: "Gowun Dodum", serif;
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

  .title {
    margin: 50px 0px;
    font-family: "Meddon", cursive;
    font-style: normal;
    font-size: 35px;
  }
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

    border-radius: 49% 49% 0% 0%;
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

.concept4 {
  padding: 60px 0 80px;
  background-color: rgba(255, 255, 255, 0.5); 

  display: flex;
  flex-direction: column;
  align-items: center;
  // border-radius: 25px 25px 0 0;
  @media (min-width: 769px) {
      border-radius:25px 25px 0 0;
    }
  .concept4-body{
    width:90%;
    height:90vh;
    background-color: #f8f8f8;
    border-radius: 25px;
   
  }
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

    width: 90%;
    height: 500px;

    display: flex;
    justify-content: center;

    overflow: hidden;

    pointer-events: none;
  }

  .sakura {
    position: absolute;

    // background: linear-gradient(
    //   135deg,
    //   #ffb7c5,
    //   #fff2f5
    // );

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

  .overlay {
    position: absolute;
    top: -30px;
    left: -100px;
    width: 500px !important;
    height:500px !important;
  }

} 

.concept5 {
  background-color: rgba(255, 255, 255, 0.5); 

  display: flex;
  flex-direction: column;
  align-items: center;
  // border-radius: 25px 25px 0 0;
  @media (min-width: 769px) {
      border-radius:25px 25px 0 0;
    }
  .photo-wrap {
    display: flex;
 
    align-items: center;
    justify-content: center;
    gap: 20px;
  }

  .photo {
    width: 100vh;
    height: 100vh;
    position: relative;
    overflow: hidden;

    border-radius: 5%;
  }

  .photo .image {
    // width: 100%;
    height: 100vh;

    object-fit: contain;
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
    top: 2%;
    width:100%;
    height: 20%;
    font-family: "Francisco";
    font-size:72px;
    color:#eeee6f;
    line-height: 1.1;
    text-shadow: -2px 0px rgb(37, 37, 37), 0px 1px rgb(14, 14, 14), 1px 0px rgb(10, 10, 10), 0px -1px rgb(3, 3, 3);
    margin:10px
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

    width: 90%;
    height: 100%;

    display: flex;
    justify-content: center;

    overflow: hidden;

    pointer-events: none;
  }

  .sakura {
    position: absolute;

    // background: linear-gradient(
    //   135deg,
    //   #ffb7c5,
    //   #fff2f5
    // );

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

<template>
  <div class="location">
    <Title title="LOCATION">
      <div class="address">
        <div>W웨딩 K웨딩홀</div>

        <div class="address-line">
          <span>{{ address }}</span>
          <img src="@/image/icon/copy.svg" class="icon" @click="copy()" />
        </div>
      </div>
    </Title>

    <div class="map-wrap">
      <div id="map" style="width: 100%; height: 250px"></div>
      <button class="map-btn" @click="moveToCurrent">초기화</button>
    </div>
    <div class="info">
      <div @click="openLink('naver')">
        <img src="@/image/map/naver.png" />네이버지도
      </div>

      <div @click="openLink('kakao')">
        <img src="@/image/map/kakao.png" />카카오 내비
      </div>
      <div @click="openLink('tmap')"><img src="@/image/map/t.png" />티맵</div>
    </div>
  </div>
  <Toast :message="toastMessage" :duration="2000" />
</template>

<script setup>
import { onMounted, ref } from "vue";
import Toast from "@/component/Toast.vue";
import Title from "@/component/Title.vue";
const map = ref(null);

let weddingLocation = null;
let markerOptions = null;
const address = "부산 연제구 중앙대로 1217 국제빌딩 4층";
onMounted(() => {
  // 네이버 지도 API 로드
  const script = document.createElement("script");
  script.src =
    "https://oapi.map.naver.com/openapi/v3/maps.js?ncpKeyId=fcmfetq61c";
  script.async = true;
  script.defer = true;
  document.head.appendChild(script);

  script.onload = () => {
    weddingLocation = new naver.maps.LatLng(35.195902, 129.079399);

    // 네이버 지도 생성
    map.value = new window.naver.maps.Map("map", {
      center: weddingLocation,
      zoom: 18,
    });

    markerOptions = {
      position: weddingLocation,
      map: map.value,
      icon: {
        url: `${window.location.host}/wedding/favicon.ico`,
        size: new naver.maps.Size(50, 52),
        origin: new naver.maps.Point(0, 0),
        anchor: new naver.maps.Point(25, 26),
      },
    };
    new naver.maps.Marker(markerOptions);
  };
});

const openLink = (pageNm) => {
  if (pageNm === "naver") {
    window.open("https://naver.me/x67yKU1M");
  } else if (pageNm === "kakao") {
    window.open("https://kko.to/F0WYUJT7U1");
  } else if (pageNm === "tmap") {
    window.open("https://tmap.life/2ca9dc17");
  }
};

const moveToCurrent = () => {
  map.value.setZoom(18, true);
  map.value.panTo(weddingLocation);
};

const toastMessage = ref("");
const copy = () => {
  navigator.clipboard
    .writeText(address)
    .then(() => {
      console.log("Text copied to clipboard...");
      toastMessage.value = "";
      requestAnimationFrame(() => {
        toastMessage.value = "주소가 복사되었습니다.";
      });
    })
    .catch((err) => {
      console.log("Something went wrong", err);
    });
};
</script>
<style lang="scss">
.location {
  position: relative; // 추가
  width: 100%;
  margin-top: 50px;
  // margin: 0 auto;

  overflow: hidden;
  height: 100%;
  transition: height 0.4s ease;

  line-height: 1.8;
}

.address {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
  margin-bottom: 40px;
}

.address-line {
  display: flex;
  align-items: center;
  gap: 6px;
}

.icon {
  width: 18px;
  height: 18px;
  cursor: pointer;
  flex-shrink: 0;
}

.info {
  background-color: rgb(255, 255, 254);
  padding: 10px;
  display: grid;
  gap: 5px;
  grid-auto-flow: column;
  cursor: pointer;

  img {
    width: 15px;
    height: 15px;
    margin-right: 5px;
  }

  div:not(:last-child) {
    border-right: 1px solid rgb(184, 183, 183);
  }
}

.icon {
  width: 15px;
  height: 15px;
}

.map-wrap {
  position: relative;
}

#map {
  width: 100%;
  height: 300px;
}

.map-btn {
  position: absolute;
  top: 12px;
  left: 12px;
  z-index: 1000;
  padding: 5px 8px;
  border: none;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  opacity: 0.8;
  cursor: pointer;
}
.map-btn:hover {
  opacity: 1;
}
</style>

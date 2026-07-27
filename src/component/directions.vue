<template>
  <div class="directions">
    <div class="directions-header">
      <img src="@/image/icon/car.svg" class="icon" /> 자차
    </div>
    <div class="directions-body">
      내비게이션 : '부산 w웨딩 K웨딩홀 검색' <br />
      부산 연제구 중앙대로 1217 국제빌딩 4층
    </div>
    <Line />
    <div class="directions-header">
      <img src="@/image/icon/bus.svg" class="icon" />
      버스
    </div>
    <div class="directions-body">
      <span><b>29,51,52,179 (세병교 방면)</b></span>
      <br />
      교대역 하차 > 도보5분
      <br />
      <br />
      <span><b>29,51,100-1,179,189 (연산역 연산교차로 방면) </b></span>
      <br />동해선 교대역 하차 > 도보 5분
      <br />
      <br />
      <span><b> 10,31,43,52,77,129-1,506 (거제 1치안센터 방면)</b></span>
      <br />동해선 교대역 하차 > 도보 3분
    </div>
    <Line />
    <div class="directions-header">
      <img src="@/image/icon/subway.svg" class="icon" />
      지하철
    </div>
    <div class="directions-body">
      <b>부산 지하철 1호선,동해선 (교대역)</b> <br />
      교대역 3,5번 출구 > 도보 1분
    </div>
    <Line />
    <div class="directions-header">
      <img src="@/image/icon/parking.svg" class="icon" />
      주차
    </div>
    <div class="directions-body">
      건물 주차장 혹은 외부 주차장 이용 <br />
      교대, 삼성, 국제, 델리 민영주차장 : 도보2분 <br />
      부산 교육대학교 주차장 : 도보 5분<br/><br/>
      주차요원의 안내를 따라주세요.<br/><br/>

      건물 주차장과 외부 주차장 주차권 받는 장소가 다르니 유의해주세요.
      <br/>
      <table class="parking" align="center" width="100%">
        <th colspan="3">건물 주차장</th>
        <tr>
            <td><b>수령처</b></td>
            <td>4층 엘레베이터</td>
            <td>뷔페 카운터</td>
        </tr>
        <tr>
            <td><b>제공시간</b></td>
            <td>1시간</td>
            <td>2시간</td>
        </tr>
       </table>
        <table class="parking" align="center" width="100%">
        <th colspan="2">
          외부 주차장<br/>
          <span style="font-weight: normal;">민영 교대, 삼성, 국제, 델리, 부산교육대</span></th>
        <tr>
            <td><b>수령처</b></td>
            <td>1층 로비 뒤쪽 후문 입구</td>
        </tr>
        <tr>
            <td><b>제공시간</b></td>
            <td>2시간</td>
        </tr>
       </table>

    </div>
  </div>
</template>
<script setup>
import Line from "@/component/Line.vue";
</script>

<style lang="scss" scoped>
.directions {
  width: 100%;
  text-align: left;
  align-self: stretch; /* 부모가 flex + align-items:center인 경우 */
  margin-bottom: 50px;
}
.directions-header {
  margin: 30px 0px;
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 16px;
}
.directions-body {
  line-height: 2;
}
.icon {
  width: 18px;
  height: 18px;
}

.parking{
  width:90%;
  // display: flex;
  // border:solid 1px black;
  border-collapse: collapse;
  margin-bottom: 10px;

  th{
    white-space: pre-line;
    background-color: var(--button-color);
  }
  th, td{
    text-align: center;
     border: 1px solid #e8e6e6;
     font-size: 12px;
    
  }
}
</style>

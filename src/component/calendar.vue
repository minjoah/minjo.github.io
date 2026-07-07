<template>
  <div class="calendar">
    <div>
      <Title title="WEDDING DAY">
        <div class="title_sub">
          <span class="ko">2026년 10월 31일 토요일 | 오후 3시 </span>
          <br />
          <span class="en">Saturday, October 31, 2026 | PM 03:00 </span>
        </div>
      </Title>

      <Line />
    </div>
    <table class="calendar_table">
      <tr>
        <th class="holidays">일</th>
        <th>월</th>
        <th>화</th>
        <th>수</th>
        <th>목</th>
        <th>금</th>
        <th class="sat">토</th>
      </tr>
      <tr v-for="week in calendarArr" :key="week">
        <td v-for="day in week" :key="day">
          <span
            :class="{
              disabled: day.isDisabled,
              'circle-number': day.isActive,
              holidays: day.isHolidays,
              sat: day.isSat,
            }"
          >
            {{ day.val }}
          </span>
        </td>
      </tr>
    </table>

    <Line />
  </div>
</template>
<script setup>
import Title from "@/component/Title.vue";
import Line from "@/component/Line.vue";
import { ref, onMounted } from "vue";
const calendarArr = ref([]);
const chunkArray = (arr, n) => {
  const result = [];
  for (let i = 0; i < arr.length; i += n) {
    result.push(arr.slice(i, i + n)); // i부터 i+n까지 잘라서 추가
  }
  return result;
};
onMounted(() => {
  const holidays = [3, 4, 5, 9, 11, 18, 25];
  const sat = [3, 10, 17, 24];
  const arr = [
    { isDisabled: true, val: 27 },
    { isDisabled: true, val: 28 },
    { isDisabled: true, val: 29 },
    { isDisabled: true, val: 30 },
  ];
  for (let i = 1; i <= 31; i++) {
    const obj = { isDisabled: false, val: i };
    if (i === 31) {
      obj.isActive = true;
    }
    if (sat.includes(i)) {
      obj.isSat = true;
    }

    if (holidays.includes(i)) {
      obj.isHolidays = true;
    }
    arr.push(obj);
  }

  calendarArr.value = chunkArray(arr, 7);
});
</script>
<style lang="scss">
.title_sub {
  margin-top: 30px;
  line-height: 1.8;
  .ko {
    color: #070707;
  }
  .en {
    color: #6c6c6c;
  }
}
.calendar {
  align-items: center;
  margin-top: 100px;
}

.calendar_table {
  width: 100%;
  margin: auto;
  text-align: center;
  table-layout: fixed;
  border-collapse: collapse;
  tr {
    height: 60px;
  }
}

.calendar_table th,
.calendar_table td {
  width: calc(100% / 7);
  text-align: center;
}
.disabled {
  color: rgb(190, 190, 190);
}

.circle-number {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  width: 25px; /* 원의 크기 */
  height: 25px; /* width와 같게 설정 */
  border-radius: 50%; /* 원형으로 만들기 */
  background-color: #070707; /* 배경색 */
  color: white; /* 숫자 색상 */
  font-weight: bold;
}

.holidays {
  color: red !important;
}

// .sat {
//   color: rgb(66, 66, 66);
// }
</style>

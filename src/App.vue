<template>
  <div id="wrap">
    <!-- <navBar /> -->
    <RouterView />
  </div>
</template>
<script setup>
import navBar from "@/navBar.vue";
</script>
<style lang="scss">
* {
  box-sizing: border-box;
  touch-action: manipulation;
}

:root {
  --bg-color: #eadaa9; /* body */
  --section1: #f4f3f3;
  --section2: #f7f0d9;
  --section3: #eae8e8;

  --bg-default: rgb(253, 253, 253);

  --button-color: #dac37f;
  --accent-color: #b89b4b;
  --text-color: #3c3c3c;
}

html,
body,
#app {
  width: 100%;
  min-height: 100%;
  margin:0;
  padding:0;

  overflow-x: hidden;
  display: flex;
  justify-content: center; /* 가로 가운데 정렬 */

  @media (min-width: 769px) {
   padding:30px 0 ;
  }
}

body {
  background-color: var(--bg-color);
}

#wrap {
  width: 100%;
  max-width: 480px;

  margin: 0 auto;
  text-align: center;
  // background: #f5f5f5;
  min-height: 100dvh;
}
</style>

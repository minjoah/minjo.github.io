<template>
    <div class="bgm-body">
        <audio
            ref="audioRef"
            src="/wedding/bgm.mp3"
            loop
            preload="auto"
        />
        <div class="audioMsg" :class="{'fade-in':isShow,'fade-out':!isShow}">
            배경음악이 준비되었습니다.
        </div>
        <div class="bgm-btn" @click="toggleBgm">
            <img v-if="isPlaying" src="@/image/icon/audio1.png"/>
            <img v-else src="@/image/icon/no_sound.png" />
        </div> 
    </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
const audioRef = ref(null)
const isPlaying = ref(true)
const isShow = ref(false)

const toggleBgm = async () => {
  if (!audioRef.value) return
  try {
    if (isPlaying.value) {
      audioRef.value.pause()
      isPlaying.value = false
    } else {
      await audioRef.value.play()
      isPlaying.value = true
    }
  } catch (e) {
    console.error(e)
  }
}

onMounted(()=>{
    isShow.value = true
    setTimeout(()=>{
        isShow.value = false
    },8000)
})
</script>
<style lang="scss" scoped>

.bgm-body{
  display: flex;
  align-items: center; /* 세로 중앙 */
  justify-content: center;
}

.bgm-btn {
  position: absolute;
  top:5px;
  right: 5px;
  bottom: 20px;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  background-color: var(--accent-color);
  opacity: 0.6;
  display: flex;
  align-items: center; /* 세로 중앙 */
  justify-content: center;

  z-index: 9999;

  img{ 
    opacity: 1 !important;
    width:20px;
    height:20px
  }
}

.audioMsg{
    position: absolute;
    top:5px;
    opacity: 0;
    background-color: black;
    padding:5px 10px;
    border-radius: 30px;
    font-size:12px;
    color:white;
    z-index: 9999;
}

.fade-in {
    opacity: 0.8;
    transition: 1s;
}

.fade-out {
    opacity: 0;
    transition: 1s;
}
</style>

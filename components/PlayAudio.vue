<template>
  <button 
    class="audio-player-btn"
    @click="togglePlay"
    :disabled="isLoading"
  >
    <!-- 加载状态 -->
    <span v-if="isLoading" class="loading">⌛</span>
    <!-- 播放状态 -->
    <span v-else-if="isPlaying">⏸️</span>
    <!-- 暂停状态 -->
    <span v-else>▶️</span>
  </button>
</template>

<script setup>
import { ref, onUnmounted } from 'vue'

// 接收外部传入的音频链接（必传）
const props = defineProps({
  audioSrc: {
    type: String,
    required: true,
    validator: (val) => {
      // 简单验证音频链接格式
      return val.startsWith('http') && (val.endsWith('.mp3') || val.endsWith('.wav') || val.endsWith('.ogg'))
    }
  }
})

// 状态管理
const audioRef = ref(null) // 音频实例引用
const isPlaying = ref(false) // 是否正在播放
const isLoading = ref(false) // 是否正在加载

// 初始化音频实例
function initAudio() {
  if (audioRef.value) return audioRef.value
  
  const audio = new Audio(props.audioSrc)
  
  // 加载开始
  audio.addEventListener('loadstart', () => {
    isLoading.value = true
  })
  
  // 加载完成
  audio.addEventListener('canplay', () => {
    isLoading.value = false
  })
  
  // 播放结束
  audio.addEventListener('ended', () => {
    isPlaying.value = false
  })
  
  // 加载失败
  audio.addEventListener('error', () => {
    isLoading.value = false
    alert('音频加载失败，请检查链接是否有效')
  })
  
  audioRef.value = audio
  return audio
}

// 切换播放/暂停
function togglePlay() {
  const audio = initAudio()
  
  if (isPlaying.value) {
    audio.pause()
    isPlaying.value = false
  } else {
    audio.play().then(() => {
      isPlaying.value = true
    }).catch((err) => {
      isLoading.value = false
      console.error('播放失败：', err)
      alert('播放失败，可能是浏览器限制或音频链接无效')
    })
  }
}

// 组件卸载时销毁音频实例
onUnmounted(() => {
  if (audioRef.value) {
    audioRef.value.pause()
    audioRef.value.remove()
    audioRef.value = null
  }
})
</script>

<style scoped>
.audio-player-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s ease;
  gap: 6px;
}

.audio-player-btn:disabled {
  background-color: #95a5a6;
  cursor: not-allowed;
  opacity: 0.7;
}

.loading {
  display: inline-block;
  animation: blink 1s infinite alternate;
}

@keyframes blink {
  from { opacity: 0.6; }
  to { opacity: 1; }
}
</style>
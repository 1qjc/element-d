<template>
  <el-progress :percentage="50" />

  <div id="audio-player-container">
    <audio
      src="https://assets.codepen.io/4358584/Anitek_-_Komorebi.mp3"
      preload="metadata"
      loop
    ></audio>
    <button id="play-icon">
      <el-icon size="30"><VideoPlay /></el-icon>
      <!-- <el-icon size="30"><VideoPause /></el-icon> -->
    </button>
    <span id="current-time" class="time">0:00</span>
    <span class="time">/</span>
    <span id="duration" class="time">0:00</span>
    <input type="range" id="seek-slider" max="100" value="0" />
    <div id="sound" style="position: relative; display: flex; flex-direction: column-reverse">
      <button id="mute-icon">
        <el-icon size="30"><Microphone /></el-icon>
        <!-- <el-icon size="30"><Mute /></el-icon> -->
      </button>
      <div>
        <output id="volume-output">10</output>
        <input type="range" id="volume-slider" max="100" value="10" />
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { onMounted } from 'vue'
/** Implementation of the functionality of the audio player */
onMounted(() => {
  /** Implementation of the presentation of the audio player */

  const playIconContainer = document.getElementById('play-icon')
  const audioPlayerContainer = document.getElementById('audio-player-container')
  const seekSlider = document.getElementById('seek-slider')
  const volumeSlider = document.getElementById('volume-slider')
  const muteIconContainer = document.getElementById('mute-icon')
  let playState = 'play'
  let muteState = 'unmute'

  playIconContainer.addEventListener('click', () => {
    if (playState === 'play') {
      audio.play()
      // requestAnimationFrame(whilePlaying)
      playState = 'pause'
    } else {
      audio.pause()
      // cancelAnimationFrame(raf)
      playState = 'play'
    }
  })

  muteIconContainer.addEventListener('click', () => {
    if (muteState === 'unmute') {
      audio.muted = true
      muteState = 'mute'
    } else {
      audio.muted = false
      muteState = 'unmute'
    }
  })

  const showRangeProgress = (rangeInput) => {
    if (rangeInput === seekSlider)
      audioPlayerContainer.style.setProperty(
        '--seek-before-width',
        (rangeInput.value / rangeInput.max) * 100 + '%'
      )
    else
      audioPlayerContainer.style.setProperty(
        '--volume-before-width',
        (rangeInput.value / rangeInput.max) * 100 + '%'
      )
  }

  seekSlider.addEventListener('input', (e) => {
    showRangeProgress(e.target)
  })
  volumeSlider.addEventListener('input', (e) => {
    showRangeProgress(e.target)
  })

  /** Implementation of the functionality of the audio player */

  const audio: HTMLAudioElement = document.querySelector('audio')!
  const durationContainer = document.getElementById('duration')
  const currentTimeContainer = document.getElementById('current-time')
  const outputContainer = document.getElementById('volume-output')
  // let raf = null
  audio.playbackRate = 1
  const calculateTime = (secs) => {
    const minutes = Math.floor(secs / 60)
    const seconds = Math.floor(secs % 60)
    const returnedSeconds = seconds < 10 ? `0${seconds}` : `${seconds}`
    return `${minutes}:${returnedSeconds}`
  }

  const displayDuration = () => {
    durationContainer.textContent = calculateTime(audio.duration)
  }

  const ssetSliderMax = () => {
    seekSlider.max = Math.floor(audio.duration)
  }

  const displayBufferedAmount = () => {
    const bufferedAmount = Math.floor(audio.buffered.end(audio.buffered.length - 1))
    audioPlayerContainer.style.setProperty(
      '--buffered-width',
      `${(bufferedAmount / seekSlider.max) * 100}%`
    )
  }

  const whilePlaying = () => {
    seekSlider.value = Math.floor(audio.currentTime)
    currentTimeContainer.textContent = calculateTime(seekSlider.value)
    audioPlayerContainer.style.setProperty(
      '--seek-before-width',
      `${(seekSlider.value / seekSlider.max) * 100}%`
    )
    raf = requestAnimationFrame(whilePlaying)
  }
  audio?.addEventListener('playing', whilePlaying)

  if (audio.readyState > 0) {
    displayDuration()
    setSliderMax()
    displayBufferedAmount()
  } else {
    audio.addEventListener('loadedmetadata', () => {
      displayDuration()
      setSliderMax()
      displayBufferedAmount()
    })
  }

  audio.addEventListener('progress', displayBufferedAmount)

  seekSlider.addEventListener('input', () => {
    currentTimeContainer.textContent = calculateTime(seekSlider.value)
    // if (!audio.paused) {
    //   cancelAnimationFrame(raf)
    // }
  })

  seekSlider.addEventListener('change', () => {
    audio.currentTime = seekSlider.value
    if (!audio.paused) {
      requestAnimationFrame(whilePlaying)
    }
  })

  volumeSlider.addEventListener('input', (e) => {
    const value = e.target.value
    outputContainer.textContent = value
    audio.volume = value / 100
  })
})
</script>
<style>
body {
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif;
  letter-spacing: -0.5px;
}
button {
  margin: 0 8px 0 0;
  padding: 0;
  border: 0;
  background: transparent;
  cursor: pointer;
  outline: none;
  width: 40px;
  height: 40px;
  float: left;
}
#audio-player-container {
  --seek-before-width: 0%;
  --volume-before-width: 10%;
  --buffered-width: 0%;
  position: relative;
  display: flex;
  align-items: end;
  margin: 200px 50px;
  width: 500px;
  height: 100px;
  background: #fff;
}
#play-icon {
}
.time {
  display: inline;
  line-height: 40px;
  text-align: center;
  font-size: 20px;
}
output {
  display: inline-block;
  width: 40px;
  text-align: center;
  font-size: 20px;
  margin-bottom: 70px;
  float: left;
  clear: left;
}
#volume-slider {
  width: 100px;
  position: relative;
  transform: rotate(270deg) translateX(35px) translateY(-45px);
}
#volume-slider::before {
  width: var(--volume-before-width);
}
#mute-icon {
}
input[type='range'] {
  position: relative;
  -webkit-appearance: none;
  width: 48%;
  margin: 0 16px;
  padding: 0;
  height: 40px;
  float: left;
  outline: none;
}
input[type='range']::-webkit-slider-runnable-track {
  width: 300px;
  height: 3px;
  cursor: pointer;
  background: rgba(0, 125, 181, 0.6);
}
#seek-slider::-webkit-slider-runnable-track {
  background: linear-gradient(
    to right,
    rgba(0, 125, 181, 0.6) var(--buffered-width),
    rgba(0, 125, 181, 0.2) var(--buffered-width)
  );
}
input[type='range']::before {
  position: absolute;
  content: '';
  top: 18.5px;
  left: 0;
  width: var(--seek-before-width);
  height: 3px;
  background-color: #007db5;
  cursor: pointer;
}
input[type='range']::-webkit-slider-thumb {
  position: relative;
  -webkit-appearance: none;
  box-sizing: content-box;
  border: 1px solid #007db5;
  height: 15px;
  width: 15px;
  border-radius: 50%;
  background-color: #fff;
  cursor: pointer;
  margin: -7px 0 0 0;
}
input[type='range']:active::-webkit-slider-thumb,
input[type='range']:hover::-webkit-slider-thumb {
  transform: scale(1.5);
  background: #007db5;
  transition: all 0.5s ease-out;
}
</style>

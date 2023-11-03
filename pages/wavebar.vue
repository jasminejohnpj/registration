<template>
    <div>
      <select class="lang" v-model="languagehome" style="width: 16.5vw">
        <option value="" disabled>Selected Languages</option>
        <option value="English">English</option>
        <option value="Malayalam">Malayalam</option>
        <option value="Tamil">Tamil</option>
        <option value="Telugu">Telugu</option>
        <option value="Kannada">Kannada</option>
        <option value="Hindi">Hindi</option>
      </select>
      <button class="playbutton" @click="togglePlay">
        <img v-if="!isPlaying" src="C:\Users\admin\Downloads\demo-reg\components\playbtn.png" alt="Play" style="width: 3.5vw; height: 8vh;" />
        <img v-else src="C:\Users\admin\demo1\components\pause-button.png" alt="Pause" style="width: 3vw; height: 9vh;" />
      </button>
      <div ref="waveform" style="width: 30%;"></div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        languagehome: '',
        isPlaying: false,
        audio: null,
        wavesurfer: null,
        audioSources: {
          English: '/audio/english.mp4', // Replace with the path to your English audio file
          Malayalam: '/audio/malayalam.mp4', // Replace with the path to your Malayalam audio file
          Tamil: '/audio/tamil.mp4', // Replace with the path to your Tamil audio file
          Telugu: '/telugu.mp4', // Replace with the path to your Telugu audio file
          Kannada: '/kannada.mp4', // Replace with the path to your Kannada audio file
          Hindi: '/audio/hindi.mp4', // Replace with the path to your Hindi audio file
        }
      };
    },
    methods: {
      async togglePlay() {
        if (!this.audio) {
          const wavesurferModule = await import('wavesurfer.js');
          this.wavesurfer = wavesurferModule.default.create({
            container: this.$refs.waveform,
            waveColor: 'violet',
            progressColor: 'purple',
            barWidth: 3,
            barHeight: 1,
            height: 100
          });
          this.wavesurfer.load(this.audioSources[this.languagehome]);
          this.audio = new Audio(this.audioSources[this.languagehome]);
        }
  
        if (this.isPlaying) {
          this.audio.pause();
          this.wavesurfer.pause();
          this.isPlaying = false;
        } else {
          this.audio.play();
          this.wavesurfer.play();
          this.isPlaying = true;
        }
      }
    }
  };
  </script>
  
  <style>
  .playbutton {
    width: 3.5vw;
    height: 8vh;
    position: relative;
    right: -38vw;
    top: 10vh;
    border: none;
    background-color: #0f0f16;
  }
  </style>
  
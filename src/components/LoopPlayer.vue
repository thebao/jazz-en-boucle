<template>
  <div class="loop-player">
    <audio :class="playerViz" ref="audioLoop" controls loop :src="source"></audio>
    <img @click="toggleMute" :class="{ muted: muted }" class="icon" :src="imageSrc"/>
    <input type="range" min="0" max="1" step="0.2" v-model="volume" />
  </div>
</template>

<script>
export default {
  name: 'LoopPlayer',
  props: {
    source: { type: String, required: true },
    name: { type: String, required: true }
  },
  data: function() {
    return {
      muted: false,
      audio: null,
      volume: 1,
      playerViz: "hidden",
    }
  },
  methods: {
    playPause: function() {
      if(this.audio.paused){
        this.audio.play();
        this.audio.currentTime = 0;
      }
      else {
        this.audio.pause();
      }
    },
    toggleMute: function() {
      return this.muted = !this.muted;
    }
  },
  computed: {
    imageSrc: function(){
      return this.name + ".png";
    }
  },
  mounted: function() {
    this.audio = this.$refs["audioLoop"];
    console.log(this.audio)
  },
  watch:{
    volume: function(value) {
      this.audio.volume = value;
    },
    muted: function(value) {
      this.audio.muted = value;
    }
  }
};
</script>

<style scoped lang="scss">
.loop-player {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 1rem;
}
.hidden {
  display: none;
}
.icon {
  transition: all 0.5s ease;
  &.muted {
    filter: grayscale(100%);
    opacity: 0.5;
  }
  width: 96px;
}
</style>

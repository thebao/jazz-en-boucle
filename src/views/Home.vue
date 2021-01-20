<template>
  <div class="home">
    <h1>Jazz-en-Boucle</h1>
    <button @click="playPause">{{ label }}</button>
    <div class="players">
      <LoopPlayer ref="son1" name="sax" source="son1.wav"></LoopPlayer>
      <LoopPlayer ref="son2" name="keys" source="son2.wav"></LoopPlayer>
      <LoopPlayer ref="son3" name="bass" source="son3.wav"></LoopPlayer>
      <LoopPlayer ref="son4" name="drums" source="son4.wav"></LoopPlayer>
    </div>
  </div>
</template>

<script>
import LoopPlayer from '@/components/LoopPlayer.vue'

export default {
  name: 'Home',
  data: function() {
    return {
      playing: false,
      label: "Démarrer"
    }
  },
  methods: {
    playPause: function() {
      if (!this.playing){
        this.label = "Arrêter";
      }
      else {
        this.label = "Démarrer";
      }
      this.$refs["son1"].playPause();
      this.$refs["son2"].playPause();
      this.$refs["son3"].playPause();
      this.$refs["son4"].playPause();
      this.playing = !this.playing;
    }
  },
  components: {
    LoopPlayer
  }
};
</script>

<style lang="scss">
body, html {
  margin: 0;
  padding: 0;
  top: 0;
}
@font-face {
  font-family: "Berkah";
  src: url("~@/assets/fonts/Berkah.ttf") format("truetype");
}
h1 {
  font-family: "Berkah";
  text-align: center;
  color: white;
  font-size: 64px;
  margin: 1rem;
}
button {
  display: inline-block;
  margin: 1rem auto;
  width: 100%;
  font-size: 1.4rem;
  text-align: center;
}
.home {
  max-width: 480px;
  margin: 0 auto;
  .players {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }
}
</style>

<template>
  <div class="synth-container">
    <div id="sequencer">
      <SynthTone v-for="chord in chords" :chord="chord" :Tone="Tone"/>
    </div>
    <div id="transport">
      <div id="toggle-play" @click="togglePlay"></div>
    </div>
  </div>
</template>

<script>
import SynthTone from "./SynthTone.vue"
import Tone from "../../node_modules/tone/build/Tone.min.js"
import bus from "../bus.js"

export default {
  name: 'SynthContainer',
  components: {
    SynthTone
  },
  data: function() {
    return {
      'chords': [['C3', 'E3'], ['D3', 'F3']],
      'Tone': Tone,
      'playing': false
    }
  },
  methods: {
    togglePlay: function() {
      if (!this.playing) {
        bus.$emit("play");
        this.playing = true;
      }
      else {
        bus.$emit("pause");
        this.playing = false;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#transport, #sequencer {
  width:100%;
}

#toggle-play {
  margin:0 auto;
  width:100px;
  height:100px;
  background-color: blue;
}
</style>

<template>
  <div class="synth-tone">
    <div class="note-container">
      <div v-for="note in notes" class="synth-note"></div>
    </div>
  </div>
</template>

<script>
import Tone from "../../node_modules/tone/build/Tone.min.js";

export default {
  name: 'SynthTone',
  props: ['chord'],
  mounted: function() {
    var synth = new Tone.PolySynth(2, Tone.Synth).toMaster();
    synth.set({
      "envelope": {
        "attack": 0.1
      }
    });

    var seq = new Tone.Sequence(function(time, noteIdx) {
      if (noteIdx) {
        synth.triggerAttackRelease(["C4", "E4"], "4n");
        synth.start();
      }
    }, this.notes, "4n").start();

    Tone.Transport.start();

  },
  data: function() {
    return {
      'notes': [false , true, true, false]
    }
  }
}
</script>

<style>
.synth-note {
  width: 200px;
  height: 50px;
  background-color: gray;
  margin:3px 3px;
  display:inline-block;
  opacity:0.5;
  transition: 0.2s;
}

.synth-note:hover {
  opacity:1;
}

</style>

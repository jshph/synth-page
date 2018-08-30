<template>
  <div class="synth-tone">
    <div class="note-container">
      <div v-for="(note, idx) in notes" class="synth-note" :class="{'step-on': note}" @click="toggleStep(idx)" ></div>
    </div>
  </div>
</template>

<script>
import bus from "../bus.js"

export default {
  name: 'SynthTone',
  props: ['chord', 'Tone'],
  mounted: function() {
    this.synth.set({
      "envelope": {
        "attack": 0.1
      }
    });

    this.Tone.Transport.start();

    bus.$on("play", function() {
      this.seq = this.initializeSeq();
      this.seq.start()
    }.bind(this));

    bus.$on("pause", function() {
      this.seq.stop();
    }.bind(this));

  },
  data: function() {
    return {
      'seq': null,
      'notes': [false , false, false, false],
      'synth': new this.Tone.PolySynth(2, this.Tone.Synth).toMaster()
    }
  },
  methods: {
    toggleStep: function(idx) {
      this.notes.splice(idx, 1, this.notes[idx] ? false : true);
    },
    initializeSeq: function() {
      return new this.Tone.Sequence(function(time, isNoteOn) {
        if (isNoteOn) {
          this.synth.triggerAttackRelease(this.chord, "1n");
        }
      }.bind(this), this.notes, "1n");
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

.synth-note:hover, .synth-note.step-on {
  opacity:1;
}

</style>

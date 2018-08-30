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
    this.synth.release = 0.4

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
    var reverb = new this.Tone.Reverb().toMaster();
    reverb.decay = 1.4;
    reverb.generate();

    return {
      'seq': null,
      'notes': [false , false, false, false],
      'synth': new this.Tone.Sampler({
        "C3": "http://127.0.0.1:3000/Yamaha-SY22-Full-Str-C2.mp3"
      }).connect(reverb)
    }
  },
  methods: {
    toggleStep: function(idx) {
      this.notes.splice(idx, 1, this.notes[idx] ? false : true);
    },
    initializeSeq: function() {
      return new this.Tone.Sequence(function(time, isNoteOn) {
        if (isNoteOn) {
          this.chord.forEach(function(key) {
            this.synth.triggerAttackRelease(key, "1n");
          }.bind(this));
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

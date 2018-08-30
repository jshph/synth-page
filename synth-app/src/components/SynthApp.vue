<template>
  <div class="synth-container">
    <SynthTone v-for="chord in chords" :chord="chord"/>
  </div>
</template>

<script>
import SynthTone from "./SynthTone.vue"

export default {
  name: 'SynthContainer',
  components: {
    SynthTone
  },
  data: function() {
    return {
      'chords': [['C4', 'E4'], ['D4', 'F4']]
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
</style>

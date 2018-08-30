<template>
  <div class="synth-tone">
    <div class="note-container">
      <div v-for="note in notes" class="synth-note"></div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'SynthTone',
  data: function() {
    return {
      'notes': [1, 2, 3, 4, 5]
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

<template>
  <div>
    <img src="../assets/logo.png">
    <h2>WDI SG Alumni Gallery</h2>
    <input v-on:input='emitFilterEvent' placeholder='type something to filter'>
  </div>
</template>

<script>
export default {
  name: 'filter',
  data: function() {
    return {
      }
    },
  methods: {
    emitFilterEvent: function(e) {
      // this.filterValue = e.target.value;
      console.log(e.target.value);
      this.$emit('triggerFilter', e.target.value)
    }
  }
}
</script>

<style scoped>
</style>

<template>
  <div id="Tache">
    <div>
      <input type="button" v-model="nameTache" class="border border-dark px-3 bg-transparent" v-on:click="onclick()">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tache',
  props: ['nameTache'],
  methods: {
    onclick (event) {
      this.$emit('clicked', this.nameTache)
    }
  }
}
</script>

<style scoped>

</style>

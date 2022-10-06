<template>
    <div class="semaine d-flex justify-content-evenly align-items-stretch m-2">

        <Jour jour="Lundi" class="jour"></Jour>
        <Jour jour="Mardi" class="jour"></Jour>
        <Jour jour="Mercredi" class="jour"></Jour>
        <Jour jour="Jeudi" class="jour"></Jour>
        <Jour jour="Vendredi" class="jour"></Jour>
        <Jour jour="Samedi" class="jour"></Jour>
        <Jour jour="Dimanche" class="jour"></Jour>
    </div>
</template>

<script>
import Jour from './Jour.vue'

export default {
  name: 'Semaine',
  components: {Jour}
}
</script>

<style scoped>
      .bg-g1{
    background-color: #1C6758;
}

.bg-g2{
    background-color: #3D8361;
}

.bg-g3{
    background-color: #D6CDA4;
}

.bg-g4{
    background-color: #EEF2E6;
}
</style>

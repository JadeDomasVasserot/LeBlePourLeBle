<template>
    <div id="jourSemaine" class="bg-g1 w-25 border border-dark ">
        <p class="border-bottom bg-g2 border-dark m-0"> {{jour}} </p>
        <div class="height500">
            <div>
                <img id="imageMeteo" src="" class="meteo w-50">
            </div>
            <div>
                <img id="imageArrosage" src="" class="arrosage w-50">
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Jour',
  props: ['jour']
}
</script>
<style scoped>
    .height500{
        min-height: 500px;
    }
    .meteo{
        max-width: 50px;
    }
</style>

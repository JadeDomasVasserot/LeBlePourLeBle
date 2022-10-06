<template>
  <div id="CalendrierApp" class="">
    <div id="head" class="d-flex justify-content-between border-bottom border-dark p-3">
      <div class="d-flex">
        <Tache nameTache="Météo" id="meteo" class="tache bg-g2" @clicked="controler"></Tache>
        <Tache nameTache="Arrosage" id="arrosage" class="tache bg-g2" @clicked="controler"></Tache>
      </div>
      <div class="d-flex">
        <Tache nameTache="+" id="ajouter" class="modification bg-g1"></Tache>
        <Tache nameTache="-" id="supprimer" class="modification bg-g1"></Tache>
        <Tache nameTache="Semaine précédente" id="prochain" class="prochain bg-g3" @clicked="controler"></Tache>
        <Tache nameTache="Semaine suivante" id="prochain" class="prochain bg-g3" @clicked="controler"></Tache>
      </div>
    </div>
    <div id="bodyCal" class="h-100">
      <Semaine class="sem1" v-show="true"></Semaine>
      <!-- <Semaine class="sem2" v-show="false"></Semaine> -->
    </div>
  </div>
  </template>
  
  <script>
  import Tache from './Tache.vue'
  import Semaine from './Semaine.vue'
  export default {
    name: 'CalendrierApp',
    components: {
      Tache,
      Semaine
    },
    data () {
      return {
        meteo: ['s', 'p', 'n', 'n', 'p', 's', 's'],
        meteoTest: false,
        arrosageTest: false,
        numSemaine: 1
      }
    },
    methods: {
      controler (value) {
        switch (value) {
          case 'Météo':
            this.controlerMeteo()
            break
          case 'Arrosage':
            this.controlerArrosage()
            break
          case 'Semaine précédente':
            this.semaineP()
            break
          case 'Semaine suivante':
            this.semaineS()
            break
          default:
            console.log('default')
        }
      },
      controlerMeteo () {
        if (!this.meteoTest) {
          this.displayMeteo()
          this.meteoTest = true
        } else {
          this.hideMeteo()
          this.meteoTest = false
        }
      },
      controlerArrosage () {
        if (!this.arrosageTest) {
          this.displayArrosage()
          this.arrosageTest = true
        } else {
          this.hideArrosage()
          this.arrosageTest = false
        }
      },
      getMeteo () {
        let token = '9c958ab66b58dea91eee4ef33a59628708b66a79f50582f07b71da47d2ac7351'
        let insee = '69123'
        let url = 'https://api.meteo-concept.com/api/forecast/daily?token=' + token + '&insee=' + insee
        fetch(url)
          .then(function (reponse) {
            return reponse
          })
          .then(function (reponse) {
            // this.meteoTab = myBlob.forecast
            // console.log(this.meteoTab)
            console.log(reponse)
          })
      },
      displayMeteo () {
        let semaine = document.querySelectorAll('#jourSemaine')
        for (let i = 0; i < semaine.length; i++) {
          let element = semaine[i].querySelector('#imageMeteo')
          if (this.meteo[i] === 's') {
            element.src = 'https://www.dici.fr/sites/dici.fr/files/styles/homepage_une_big/public/2016/05/22/793013-meteo-soleil-300x291.gif?itok=pZG8F019'
          }
          if (this.meteo[i] === 'n') {
            element.src = 'data:image/jpeg;base64,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'
          }
          if (this.meteo[i] === 'p') {
            element.src = 'https://static01.nicematin.com/media/npo/1440w/2014/02/61b19da99bcd6a1dd49dac11a8f9d4bf.png'
          }
          // console.log(element)
        }
      },
      hideMeteo () {
        let semaine = document.querySelectorAll('#jourSemaine')
        for (let i = 0; i < semaine.length; i++) {
          let element = semaine[i].querySelector('#imageMeteo')
          element.src = ''
        }
      },
      displayArrosage () {
        let semaine = document.querySelectorAll('#jourSemaine')
        for (let i = 0; i < semaine.length; i++) {
          let element = semaine[i].querySelector('#imageArrosage')
          if (this.meteo[i] === 's') {
            element.src = 'https://lespetitsradis.fr/img/cms/Fiches%20l%C3%A9gumes/M%C3%A2che/arroser.PNG'
          }
          if (this.meteo[i] === 'n') {
            element.src = 'https://lespetitsradis.fr/img/cms/Fiches%20l%C3%A9gumes/M%C3%A2che/arroser.PNG'
          }
        }
      },
      hideArrosage () {
        let semaine = document.querySelectorAll('#jourSemaine')
        for (let i = 0; i < semaine.length; i++) {
          let element = semaine[i].querySelector('#imageArrosage')
          element.src = ''
        }
      },
      semaineS () {
        // let sem = document.querySelector('#bodyCal').getElementsByClassName('sem' + this.numSemaine)[0]
      },
      semaineP () {
        // let sem = document.querySelector('#bodyCal').getElementsByClassName(this.numSemaine)
      }
    }
  }
  </script>
  
  <style scoped>


  </style>
  
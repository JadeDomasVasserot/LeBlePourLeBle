<template>
  <div id="StockList">
    <div class="container" v-if="true">
      <div class="card card-produit" style="width: 18rem;" v-for="produit in produits['hydra:member']" :key="produit.ID">
        <img :src="produit.photo" class="card-img-top" alt="produitPhoto" />
        <div class="card-body">
          <h5 class="card-title">{{produit.nom}}</h5>
          <p class="card-text">
            {{produit.description}}
          </p>
        </div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Quantité : {{produit.quantite}}</li>
        </ul>
        <div class="card-body">
          <button class="btn btn-success" @click="addProduit(produit.ID)">Ajouter 10</button>
          <button class="btn btn-success" @click="deleteProduit(produit.ID, produit.quantite)">Enlever 10</button>
          <router-link :to="{name: 'StockModif', params: {ModifId: produit.ID}}">Modification</router-link>
        </div>
      </div>
    </div>
    <div class="container" v-else>
     <h1>Pas de produit référencé</h1> 
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "StockList",
  data() {
    return {
      produits: axios
        .get("http://127.0.0.1:8000/api/produits")
        .then(rep => (this.produits = rep.data)),
    };
  },
  methods: {
    addProduit(ID){
        axios
        .post("http://127.0.0.1:8000/produit/ajout/"+ID+"/10");
        window.location.reload()

    },
    deleteProduit(ID, quantite){
      if(quantite >= 10){
        axios
        .post("http://127.0.0.1:8000/produit/ajout/"+ID+"/-10");
        window.location.reload()
      }
      else {
        alert("Vous ne pouvez pas supprimer une quantité en dessous de 10")
      }
    },
  }
};
</script>

<style scoped>
  .card-produit{
    margin-top: 5%;
    margin-left: 40%;
    margin-right: 40%;

  }
</style>

<template>
<div id="StockModif">
  <div class="container">
      <form class="row g-3" @submit.prevent="getFormValues" action="" method="POST">
        <div class="col-md-6">
          <label for="inputNom" class="form-label">Nom du produit</label>
          <input type="text" class="form-control" id="inputNom" name="name" :value="produitSelect.nom"/>
        </div>
        <div class="col-md-6">
          <label for="inputPhoto" class="form-label">Photo du produit</label>
          <input type="text" class="form-control" id="inputPhoto" name="photo" :value="produitSelect.photo"/>
        </div>
        <img :src="produitSelect.photo" alt="img">
        <div class="col-12">
          <label for="inputDescription" class="form-label"
            >Description courte</label
          >
          <input
            type="text"
            class="form-control"
            id="inputDescription"
            name="description"
            :value="produitSelect.description"
          />
        </div>
        <div class="col-md-3">
          <label for="inputQuantite" class="form-label">Quantité</label>
          <input type="number" class="form-control" id="inputCity" name="quantite" :value="produitSelect.quantite"/>
        </div>
        <div class="col-12">
          <input type="submit" id='submit' value='VALIDER' class="btn btn-success">
        </div>
      </form>
    </div>
</div>
</template>

<script>
import axios from 'axios';
const headers = {
    "Content-Type": "application/json",
};
export default {
  name: "StockModif",
  props:['ModifId'],
  data () {
    return {
      produitSelect: axios.get("http://127.0.0.1:8000/api/produits/"+ this.ModifId)
        .then(rep => (this.produitSelect = rep.data)),
      }
},
  methods:{
      async getFormValues (submitEvent) {
          await axios.put('http://127.0.0.1:8000/api/produits', { 
            nom: submitEvent.target.elements.name.value,
            description: submitEvent.target.elements.description.value,
            photo: submitEvent.target.elements.photo.value,
            quantite: submitEvent.target.elements.quantite.value,
          },{headers}).then(function (response) {
              console.log(response);
              
          })
          .catch(function (error) {
              console.log(error);
          });
          this.$router.push('/stock')
          
          }
      
      },
  
}
</script>

<style scoped>

</style>
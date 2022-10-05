<template>
  <div id="StockCreate">
    <div class="container">
      <form class="row g-3" @submit.prevent="getFormValues" action="" method="POST">
        <div class="col-md-6">
          <label for="inputNom" class="form-label">Nom du produit</label>
          <input type="text" class="form-control" id="inputNom" name="name" />
        </div>
        <div class="col-md-6">
          <label for="inputPhoto" class="form-label">Photo du produit</label>
          <input type="text" class="form-control" id="inputPhoto" name="photo"/>
        </div>
        <div class="col-12">
          <label for="inputDescription" class="form-label"
            >Description courte</label
          >
          <input
            type="text"
            class="form-control"
            id="inputDescription"
            name="description"
          />
        </div>
        <div class="col-md-3">
          <label for="inputQuantite" class="form-label">Quantité</label>
          <input type="number" class="form-control" id="inputCity" name="quantite"/>
        </div>
        <div class="col-12">
          <input type="submit" id='submit' value='VALIDER' class="btn btn-success">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "StockCreate",
  data () {
    return {
    }},
    methods:{
    async getFormValues (submitEvent) {
        await axios.post('http://127.0.0.1:8000/api/produits', { 
          nom: submitEvent.target.elements.name.value,
          description: submitEvent.target.elements.description.value,
          photo: submitEvent.target.elements.photo.value,
          quantite: submitEvent.target.elements.quantite.value,
        }
        ).then(function (response) {
            console.log(response);
            
        })
        .catch(function (error) {
            console.log(error);
        });
        this.$router.push('/stock')
         
        }
    
    },
};
</script>

<style scoped>
  #StockCreate{
    margin-top:1%;
  }
</style>

<template>
<div id="NavBar">
  <nav>
    <div class="container-fluid">
      <router-link to="/stock">Liste</router-link>
      <router-link to="/create">Création</router-link>
      <router-link to="/qr-code"><img width="25px" src="@/assets/icons/qr-code.svg" alt=""></router-link>
  </div>
</nav>
</div>
</template>

<script>
export default {
  name: "NavBar"
}
</script>

<style scoped>
#NavBar{
  background-color: #D6CDA4;
  
}
.container-fluid{
  justify-content: space-around;
}
a{
  color:white;
  text-decoration: none;
  font-size: 26px;
  margin-right: 1%;
  margin-left: 1%

}
</style>

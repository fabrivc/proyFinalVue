<template>
  <div id="app">
    <div v-if="!canAccess">
     <ul class="nav nav-pills nav-justified mb-3">
        <li class="nav-item">
          <a class="navbar-toggler active" data-mdb-toggle="pill" @click="cambiardeRutaLogin" role="tab" aria-controls="pills-login" aria-selected="true">Login</a>
        </li>
        <li class="nav-item">
          <a class="navbar-toggler" data-mdb-toggle="pill" @click="cambiardeRutaLogin" role="tab" aria-controls="pills-register" aria-selected="false">Register</a>
        </li>
      </ul>

      <login-page 
      v-show="estoyEnLogin"
      @changeFlag="recibiElMensaje" 
      :users="usersList"/>
    
      <register-page 
      v-show="!estoyEnLogin"
      @enviarRegistro="recibiRegistro" 
      />

    </div>

  <div v-else>
    <main-page 
    v-if="canAccess" 
    @changeFlagFromMain="recibiElMensaje" 
    :products="productsList"
    @emitVerDetalle="recibiVerDetalle"
    @emitAgregarAlCarrito="recibiAgregarAlCarrito"
    @emitLogout="recibiLogout"

    />
    
    <cart-page :carro='carrito' @emitActualizarCarritoPrincipal="recibiActualizarAlCarrito"/>
    
    <products-detail-page v-if="selected" :product="selected"/>

    </div>
</div>



</template>

<script>

import loginPage from "./components/loginPage.vue";
import registerPage from "./components/registerPage.vue";
import cartPage from "./components/cartPage.vue";
import productsDetailPage from "./components/productsDetailPage.vue";
import mainPage from "./components/mainPage.vue";
import CartPage from "./components/cartPage.vue";
import LoginPage from "./components/loginPage.vue";
import RegisterPage from "./components/registerPage.vue";
import MainPage from "./components/mainPage.vue";
import ProductsDetailPage from "./components/productsDetailPage.vue";


export default {
  name: "App",
  components: {
    loginPage,
    registerPage,
    cartPage,
    productsDetailPage,
    mainPage,
    CartPage,
    LoginPage,
    RegisterPage,
    MainPage,
    ProductsDetailPage
},
  data() {
    return {
      canAccess: false,
      estoyEnLogin:true,
      usersList: [],
      productsList: [
        {
          id: 1,
          titulo: "Flour - Chickpea",
          descripcion: "Supplement Left 5th Toe with Synth Sub, Open Approach",
          cantidad: "1",
          precio: "$2.08",
          imagen:
            "https://robohash.org/totampariaturtempore.png?size=50x50&set=set1",
        },
        {
          id: 2,
          titulo: "Sage Ground Wiberg",
          descripcion: "Supplement Right Rib with Synth Sub, Perc Approach",
          cantidad: "1",
          precio: "$5.90",
          imagen:
            "https://robohash.org/praesentiumofficiisipsum.png?size=50x50&set=set1",
        },
        {
          id: 3,
          titulo: "Pork - Bacon, Sliced",
          descripcion: "Bypass R Foot Vein to Low Vein w Nonaut Sub, Open",
          cantidad: "1",
          precio: "$0.22",
          imagen: "https://static.abc.es/media/salud/2019/04/17/bacon-cancer-knrB--620x349@abc.jpg",
        },
      ],
      carrito: [],
      selected: null,
    };
  },
  methods:{
    recibiElMensaje(){
      this.canAccess = !this.canAccess
    },
    recibiElRegistro(payload){
this.usersList.push(payload)
    },
    recibiAgregarAlCarrito(payload){
this.carrito.push(payload)
    },
    recibiActualizarCarrito(payload){
      this.carrito = payload
    },
    recibiVerDetalle(payload){
      this.selected = payload
    },
     cambiardeRutaLogin(){
      this.estoyEnLogin = !this.estoyEnLogin;
    }, 
    recibiLogout(){
      this.canAccess = !this.canAccess
    },
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

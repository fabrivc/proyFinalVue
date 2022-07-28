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

      <Login 
      v-show="estoyEnLogin"
      @changeFlag="recibiElMensaje" 
      :usuarios="listadoDeUsuarios"/>
    
      <Register 
      v-show="!estoyEnLogin"
      @enviarRegistro="recibirRegistro" 
      @emit-agregar-usuario="addUsuarioTabla"/>
    </div>
    
    <div v-else>
    <Main
    v-if="canAccess" 
    @changeFlagFromMain="recibiElMensaje" 
    :productos="listadoDeProductos"
    @emitVerDetalle="recibirVerDetalle"
    @emitAgregarAlCarrito="recibirAgregarAlCarrito"/>
    
    <Cart :carro='carrito' @emitActualizarCarritoPrincipal="recibirActualizarAlCarrito"/>
    
    <Detail v-if="selected" :producto="selected"/>

    </div>
</div>
</template>

<script>
import Login from './components/Login.vue'
import Main from './components/Main.vue'
import Register from './components/Register.vue'
import Cart from './components/Cart.vue'
import Detail from './components/Detail.vue'


export default {
  name: 'App',
  components: {
    Login,Main,Register,Cart,Detail
  },
  data(){
    return{
    canAccess:false,
    estoyEnLogin:true,
    listadoDeUsuarios:[],
    listadoDeProductos:[{
  "id": 1,
  "titulo": "Brownie",
  "descripcion": "Postre de chocolate",
  "cantidad": 74,
  "precio": 23.76,
  "imagen": "https://images.aws.nestle.recipes/original/2020_06_03T13_21_43_mrs_ImageRecipes_147427lrg.jpg"
}, {
  "id": 2,
  "titulo": "Helado",
  "descripcion": "Postre frio de diferentes gustos",
  "cantidad": 53,
  "precio": 14.03,
  "imagen": "https://rapanui.com.ar/media/catalog/product/cache/17740dc71becde9a2e44e4a7c359d4cd/1/_/1_kilo.png"
}, {
  "id": 3,
  "titulo": "Panqueques",
  "descripcion": "Postre de masa con dulce de leche",
  "cantidad": 25,
  "precio": 69.84,
  "imagen": "https://img-global.cpcdn.com/recipes/14bc6c5ef2e509ee/400x400cq70/photo.jpg"
}, {
  "id": 4,
  "titulo": "Churros",
  "descripcion": "Churros",
  "cantidad": 41,
  "precio": 4.47,
  "imagen": "https://i.pinimg.com/474x/4c/0c/5a/4c0c5a31141421a9cf7f5b3d66bdb70f.jpg"
}, {
  "id": 5,
  "titulo": "Facturas",
  "descripcion": "Facturas",
  "cantidad": 85,
  "precio": 83.36,
  "imagen": "https://ver.rosario.gob.ar/media/cache/3f/b1/3fb1aaa280925fc390b5f64cf9c54411.png"
},{
  "id": 6,
  "titulo": "Facturas",
  "descripcion": "Facturas",
  "cantidad": 85,
  "precio": 83.36,
  "imagen": "https://ver.rosario.gob.ar/media/cache/3f/b1/3fb1aaa280925fc390b5f64cf9c54411.png"
}],
    carrito:[],
    selected: null
    }
  },
  addUsuarioTabla(usuario) {
            console.log(usuario);
            const nuevoUsuario = {...usuario};
            this.usuarios.push(nuevoUsuario);
        },
  methods:{
    recibiElMensaje(){
      this.canAccess = !this.canAccess
    },
    recibirRegistro(payload){
      this.listadoDeUsuarios.push(payload)
    },
    recibirAgregarAlCarrito(payload){
      this.carrito.push(payload)
    },
    recibirActualizarAlCarrito(payload){
          //this.carrito = [...payload]
          this.carrito = Object.assing(this.carrito,payload)
    },
    recibirVerDetalle(payload){
      this.selected = payload
    },
    cambiardeRutaLogin(){
      this.estoyEnLogin = !this.estoyEnLogin;
    }
  }
}
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

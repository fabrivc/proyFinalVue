<template>
  <div>

<div class="card">
  <div class="card-body">
    <ul>
      <li v-for="item in products" :key="item.id">
      {{item.imagen}} {{item.titulo}} {{item.precio}}
      </li>
      <button @click="agregarAlCarrito(item)">Agregar a carrito</button>
      <button @click="verDetalle(item)">Ver detalle del producto</button>
    </ul>
  </div>
</div>

    <a @click="logout">Logout</a>
  </div>
</template>

<script>

export default {
  name: "mainPage",
  props: ["products"],
  data() {
    return {};
  },
  methods: {
    logout() {
      this.$emit("emitLogout");
    },
    agregarAlCarrito(payload) {
      let objetoCarrito = {...payload,cantidadCarrito: 1}
      this.$emit("emitAgregarAlCarrito", objetoCarrito);
    },
    verDetalle(payload){
      this.$emit("emitVerDetalle" , payload)
    }
  },
};
</script>


<style>
</style>
<template>
  <div>
    <ul>
        <li v-for="item in carroLocal" :key="item.id">
            <p>{{item.titulo}}</p>
            <p>{{item.cantidadCarrito}}</p>
            <button @click="sumarUno(item)">+</button>
            <button @click="restarUno(item)">-</button>
        </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: "cartPage",
  props: ["carro"],
  data() {
    return {
carroLocal: []
    };
  },
  mounted(){
    this.carroLocal = this.carro
  },
  methods: {
    remover(id) {
      this.$emit('remover' , id);
    },
    sumarUno(payload){
        payload.cantidadCarrito++
    },
    restarUno(payload){
        payload.cantidadCarrito--
    },
  },
  watch:{
    carroLocal(newObj,oldObj){
        console.log(oldObj)
        this.$emit("emitActualizarCarritoPrincipal" , newObj)
    }
  }
}
</script>

<style>
</style>


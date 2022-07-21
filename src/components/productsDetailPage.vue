<template>
  <div>
    <h1>{{product.titulo}}</h1>
    <p><i>{{product.descripcion}}</i></p>
  </div>
</template>

<script>

export default {
  name: "productsDetailPage",
  props: ["product"],
  data() {
    return {

    }
  },
}
</script>


<style>
</style>

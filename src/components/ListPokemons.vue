<script setup>
const pokemon = defineProps([
  "name",
  "foto"
]);
</script>

<template>
  <div class="col-12 col-sm-6">
    <div class="card mb-3 card_pokemon">
      <p class="text-center">{{ pokemon.name }}</p>
      <img :src="pokemon.foto" class="card-img-top imagem_pokemnon">
    </div>
  </div>
</template>

<style scoped>
.card_pokemon {
  padding: 0.5rem;
  background: rgb(51, 112, 227);
  background: radial-gradient(circle, rgba(48, 86, 220, 0.6) 0%, rgba(95, 91, 217, 0.2) 100%);
  cursor: pointer;
}

.card_pokemon:hover {
  background: radial-gradient(circle, rgba(95, 91, 217, 0.2) 100%, rgba(48, 86, 220, 0.6) 0%);
}

.card_pokemon img:hover {
  scale: 1.05;
}

.imagem_pokemnon {
  height: 80px;
  width: auto;
}
</style>
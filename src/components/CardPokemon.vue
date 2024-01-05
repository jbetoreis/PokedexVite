<script setup>
const pokemon = defineProps([
  "name",
  "xp",
  "heigth",
  "image",
  "loading",
]);
</script>

<template>
  <div class="card card_view_pokemon" :class="loading ? '' : 'animate__animated animate__flipInY'">
    <img v-if="pokemon.name" :src="pokemon.image" class="card-img-top">
    <img v-else="pokemon.name" src="../assets/egg_pokemon.svg" class="card-img-top">
    <div class="card-body">
      <h5 class="card-title text-center">{{ pokemon.name || '???' }}</h5>
      <hr>
      <div class="row">
        <section class="col text-center">
          <strong>XP: </strong>
          <span>{{ pokemon.xp || '???' }}</span>
        </section>
        <section class="col text-center">
          <strong>Altura: </strong>
          <span>{{ pokemon.heigth || '???' }}</span>
        </section>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card_view_pokemon {
  width: 100%;
  max-height: 80vh;
  background: radial-gradient(circle, rgba(220, 194, 106, .8) 0%, rgba(244, 0, 0, .8) 100%);
}

.card_view_pokemon img {
  padding: 0.5rem;
  width: auto;
  height: 15rem;
  margin: 0 auto;
}
</style>
<script setup>
import { ref, onMounted, reactive, computed } from "vue";
import ListPokemons from "../components/ListPokemons.vue";
import CardPokemon from "../components/CardPokemon.vue";

let urlBasePokemon = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/");
let pokemons = reactive(ref());
let pokemonTarget = reactive(ref());
let searchPokemon = ref("");
let loading = ref(false);

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
    .then(res => res.json())
    .then(res => {
      pokemons.value = res.results
    })
})

const pokemonsFiltered = computed(() => {
  if (pokemons.value && searchPokemon.value) {
    return pokemons.value.filter(pokemon =>
      pokemon.name.toLowerCase().includes(searchPokemon.value.toLowerCase())
    );
  }
  return pokemons.value;
});

const selectPokemon = async (pokemon) => {
  loading.value = true;
  await fetch(pokemon.url)
    .then(res => res.json())
    .then(res => {
      pokemonTarget.value = res;
    })
    .catch(err => alert(err))
    .finally(() => {
      loading.value = false;
    })
}
</script>

<template>
  <main>
    <div class="container">
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6 d-flex justify-content-center">
          <CardPokemon :name="pokemonTarget?.name" :xp="pokemonTarget?.base_experience" :heigth="pokemonTarget?.height"
            :image="pokemonTarget?.sprites.other.dream_world.front_default" :loading="loading" />
        </div>
        <div class="col-sm-12 col-md-6 d-flex justify-content-center">
          <div class="card card_lista_pokemons" style="width: 100%;">
            <div class="card-body">
              <div class="row">
                <div class="input-group mb-3">
                  <span class="input-group-text" id="basic-addon1"><i class="bi bi-search"></i></span>
                  <input type="text" class="form-control" id="searchPokemon" v-model="searchPokemon"
                    placeholder="Pesquisar...">
                </div>

                <ListPokemons v-for="pokemon in pokemonsFiltered" :key="pokemon.name" :name="pokemon.name"
                  :foto="urlBasePokemon + pokemon.url.split('/')[6] + '.svg'" @click="selectPokemon(pokemon)" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  margin-bottom: 5rem;
}

.card_lista_pokemons {
  max-height: 80vh;
}

.card_lista_pokemons {
  overflow-y: auto;
}
</style>
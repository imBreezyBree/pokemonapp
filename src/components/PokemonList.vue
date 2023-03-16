<!-- 
<template>
  <div class="flex flex-col space-y-4">
    <Pokemon
      :pokemon="pokemon"
      v-for="(pokemon, index) in pokemons"
      :key="index"
    />
  </div>
</template>

<script setup>
// import pokemons from "@/assets/sampledataset.json"
import Pokemon from "./Pokemon.vue";
import { ref, onMounted } from "vue";
import client from "@/assets/apiclient.js";
// mount and then make api call
const pokemons = ref([]);
onMounted(() => {
  client
    .get("/pokemon")
    .then((res) => {
      console.log("response received", res.data);
      pokemons.value = res.data;
    })
    .catch((errors) => {
      console.log("error", errors);
    });
});
</script>
 -->

 <template>
  <div class="flex flex-wrap justify-center">
    <div
      v-for="(pokemon, index) in pokemonList"
      :key="index"
      class="w-60 p-2"
    >
      <router-link
        :to="{ name: 'PokemonDetails', params: { name: pokemon.name } }"
      >
        <div class="bg-gray-200 rounded-lg p-2">
          <img :src="pokemon.image" :alt="pokemon.name" class="w-full" />
          <div class="text-center">{{ pokemon.name }}</div>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import client from "@/assets/apiclient.js";

const pokemonList = ref([]);

onMounted(() => {
  client.get(`/pokemon`)
    .then((res) => {
      console.log("response received", res.data);
      pokemonList.value = res.data.results.map((pokemon) => ({
        name: pokemon.name,
        image: `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.url.split('/')[6]}.png`
      }));
    })
    .catch((errors) => {
      console.log("error", errors);
    });
});
</script>

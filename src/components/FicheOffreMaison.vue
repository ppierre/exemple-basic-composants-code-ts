<script setup lang="ts">
import Bed from "./icones/Bed.vue";
import Bath from "./icones/Bath.vue";
import Size from "./icones/Size.vue";
import Heart from "./icones/Heart.vue";
import AddressRdf from "./AddressRdf.vue";

defineProps({
  id: String, //TODO type uuid
  /** nom du logement */
  nom: String,
  prix: Number,
  favori: Boolean,
  image: String,
  /** nombre de lits du logement */
  nbrLits: Number,
  /** nombre de salle de bain du logement */
  nbrSDB: Number,
  adresse: Object,
  /** Surface habitable TODO: https://schema.org/floorSize ? */
  surface: String,
});
</script>

<template>
  <figure>
    <img class="rounded-t-lg w-full h-48 object-cover" :src="image" alt="" />
    <figcaption
      class="relative flex flex-col border-2 border-t-0 rounded-b-lg px-5 py-7 border-indigo-100"
    >
      <div
        class="w-12 h-12 grid place-items-center border-2 border-indigo-100 rounded-full absolute top-7 right-5"
      >
        <Heart :class="{ 'fill-red-300': favori }" />
      </div>
      <h3 class="text-2xl text-gray-900">{{ nom }}</h3>
      <AddressRdf class="not-italic text-gray-500" :addr="adresse" short />
      <div class="flex items-center order-first">
        <div class="text-2xl font-bold text-indigo-500 pr-1">${{ prix }}</div>
        <div>/ months</div>
      </div>
      <hr class="border-indigo-100 border-t-2 my-4" />
      <div class="flex justify-between text-sm text-gray-500">
        <div><Bed class="inline-block pr-1" />{{ nbrLits }}&nbsp;Beds</div>
        <div><Bath class="inline-block pr-1" />{{ nbrSDB }} Bathrooms</div>
        <div><Size class="inline-block pr-1" />{{ surface }}</div>
      </div>
    </figcaption>
  </figure>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const imagem = ref([]);

const getImgens = async () => {
  const resposta = await axios.get("https://pixabay.com/api/?key=37298216-cbba297a2176659fc030715a4&q=yellow+flowers&image_type=photo");

  imagem.value = resposta.data.hits;
  // console.log(imagem.value);
}
</script>

<template>
  <!-- header -->
  <div>

  </div>
  <!-- a função de puxar as imagens da API e colocar um pesquisa de imagens -->
  <main class="h-screen bg-blue-300">
    <input class="border-2 rounded-md border-red-600" type="text"/>
    <button class="px-4 py-2 bg-black text-white font-bold rounded-md hover:bg-gray-700" @click="getImgens">
      Clique aqui
    </button>
    <div class="columns-3">
      <img class="m-3 hover:scale-105 hover:duration-700" :src="img.webformatURL" v-for="img in imagem">
    </div>
  </main>
</template>


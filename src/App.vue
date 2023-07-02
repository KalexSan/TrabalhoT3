<script setup>
import { ref } from "vue";
import axios from "axios";

const imagem = ref([]);
const query = ref("");

const getImgens = async () => {
  const resposta = await axios.get("https://pixabay.com/api/?key=37298216-cbba297a2176659fc030715a4&q=yellow+flowers&image_type=photo");

  imagem.value = resposta.data.hits;
  // console.log(imagem.value);
}

return {
  imagens,
  query,
  getImgens
}
</script>

<template>
  <div>
    <!-- cabeçalho -->

    <!-- O campo de busca de imagens -->
    <input class="border-2 rounded-md border-red-600" type="text" v-model="query" />

    <!-- O botão para acionar a busca de imagens -->
    <button class="px-4 py-2 bg-black text-white font-bold rounded-md hover:bg-gray-700" @click="getImgens">
      Clique aqui
    </button>

    <!-- A grade de imagens -->
    <div class="grid grid-cols-3 gap-3 m-3">
      <img class="hover:scale-105 hover:duration-700" :src="img.webformatURL" v-for="img in imagens"
        :alt="img.tags" />
    </div>
  </div>
</template>


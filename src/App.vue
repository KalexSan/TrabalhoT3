<script setup>
import { ref, watch } from "vue";
import axios from "axios";

const imagens = ref([]);
const userDig = ref("");
const paginaAtual = ref(1);

const getImgens = async () => {
  const resposta = await axios.get('https://pixabay.com/api/?key=37298216-cbba297a2176659fc030715a4&q='+ encodeURIComponent(userDig.value) +'&image_type=photo&page=' + paginaAtual.value);

  imagens.value = imagens.value.concat(resposta.data.hits);

  // console.log(imagem.value);
}

const buscarMaisImagens = () => {
  paginaAtual.value++;
  getImgens();
}

watch(userDig, async (newValue, oldValue) => {
    if (newValue == oldValue) {
      return;
    }
    paginaAtual.value = 1;
    imagens.value = [];
})

</script>

<template>
  <div>
    <div class="flex flex-col items-center m-4">
        <h1 class="m-4 text-2xl font-bold font-serif">
          Busca de imagens para baixar
        </h1>
      <div>
        <!-- O campo de busca de imagens -->
        <input class="border-2 rounded-md border-red-600 m-3" type="text" v-model="userDig" />

        <!-- O botão para acionar a busca de imagens -->
        <button class="px-4 py-2 bg-black text-white font-bold rounded-md hover:bg-gray-800" @click="getImgens">
          Clique aqui
        </button>
      </div>
    </div>
    <!-- A grade de imagens -->
    <div class="columns-xs">
      <img class="hover:scale-105 hover:duration-700 m-1" :src="img.webformatURL" v-for="img in imagens" />
    </div>
     <!-- Botão para buscar mais imagens -->
     <div class="flex justify-center mt-4">
      <button class="px-4 py-2 m-4 bg-black text-white font-bold rounded-md hover:bg-gray-800" @click="buscarMaisImagens">
        Carregar mais imagens
      </button>
    </div>
  </div>
</template>


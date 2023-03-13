<template>
  <div>
    <h1 class="text-gray-500 text-3xl font-bold mb-10">Anime Finder</h1>
    <form class="mx-auto max-w-xl flex justify-center items-center gap-4">
      <label
        for="email"
        class="block  text-sm font-medium text-gray-900 dark:text-white"
        ></label
      >
      <input
        type="email"
        id="email"
        class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
      />
      <button
        type="submit"
        @click.prevent="searchAnime"
        class="flex text-center  justify-center max-w-full w-full max-w-max text-white bg-yellow hover:bg-gray-dark transition ease-linear delay-400"
      >
        Search
      </button>
    </form>
    <div v-if="searchResult.data.length > 0">
      <div class="max-w-lg grid grid gap-4 grid-cols-4 max-w-5xl mt-10">
        <article v-for="anime in searchResult.data" :key="anime">
          <img
            :src="anime.images.webp.image_url"
            :alt="anime.title"
            class="h-60 w-full rounded-md"
          />
          <h3 class="text-bol transition ease-in">{{ anime.title }}</h3>
        </article>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import axios from "axios";

const query = ref("");
const myAnime = ref("");
const searchResult = ref("");
// const animeList = ref('')

const myAnimeList = computed(() => {
  return myAnime.value.sort((a, b) => {
    return a.title.localCompare(b.title);
  });
});

async function searchAnime() {
  const res = await axios.get(
    `https://api.jikan.moe/v4/anime?q=${query.value}`
  );
  searchResult.value = res.data;
  console.dir(res);
}
searchAnime();

// const searchAnime =  () => {

//   const url = `https://api.jikan.moe/v4/anime?q=${query.value}`
//   fetch(url)
//     .then(res => res.json())
//     .then(res => {
//       searchResult.value = res.data
//     })
// }

// const handleInput = e => {
//   if()
// }
</script>

<style lang="scss"></style>

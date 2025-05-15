<template>
  <div class="flex flex-col gap-2 items-center justify-center h-full pt-10">
    <h1 class="text-3xl font-bold underline">Hello world!</h1>
    <input class="border" type="text" v-model="search" />
    <button class="border" @click="fetchMovie">Search</button>
    <div class="max-w-full">{{ JSON.stringify(film) || "" }}</div>
  </div>
</template>

<script setup lang="ts">
import type { Movie } from "~/types/index.ts";

const search = useState<string>("search", () => "");
const film = useState<Movie | null>("res", () => null);

const fetchMovie = async (): Promise<void> => {
  console.log(search.value);
  const res = await fetch(
    `http://www.omdbapi.com/?apikey=1390f7ad&t=${search.value}`
  );
  console.log(res);

  film.value = await res.json();
};
</script>

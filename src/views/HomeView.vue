<template>
  <label> Type Country Name</label>
  <input class="country__search" type="text" v-model="search" />
  <select class="country__filter" v-model="filter">
    <option value="asia">Asia</option>
    <option value="americas">America</option>
    <option value="europe">Europe</option>
    <option value="oceania">Oceania</option>
  </select>
  <ContryList :posts="searchNames" />
</template>

<script setup>
import ContryList from "../components/ContryList.vue";
import { computed, onMounted, ref, watchEffect } from "vue";

const posts = ref([]);
const err = ref(null);
const search = ref("");
const filter = ref("");

const searchNames = computed(() => {
  return posts.value.filter((name) => name.name.common.includes(search.value));
});
console.log(typeof searchNames);
onMounted(async () => {
  try {
    let data = await fetch("https://restcountries.com/v3.1/all");
    if (!data.ok) {
      throw Error("no data available");
    }
    posts.value = await data.json();
    console.log(posts);
  } catch {
    err.value = err.message;
    console.log(err.value);
  }
});

watchEffect(async () => {
  try {
    let data = await fetch(
      `https://restcountries.com/v3.1/region/${filter.value}`
    );
    if (!data.ok) {
      throw Error("no data available");
    }
    posts.value = await data.json();
  } catch {
    err.value = err.message;
  }
}, filter.value);
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  padding: 20px;
  background: rgb(2, 0, 36);
  background: linear-gradient(
    90deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(9, 9, 121, 1) 35%,
    rgba(0, 212, 255, 1) 100%
  );
}
li {
  list-style-type: none;
}
label {
  color: white;
  font-size: 18px;
}
.country__search {
  padding: 5px 5px;
  margin-bottom: 20px;
  margin-left: 10px;
  border: none;
  border-radius: 4px;
}
.country__filter {
  padding: 5px;
  width: 150px;
  margin-left: 20px;
  border: none;
  border-radius: 4px;
}

img {
  width: 100%;
  object-fit: cover;
  height: 250px;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}
a {
  text-decoration: none;
  color: inherit;
}
</style>

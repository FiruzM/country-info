<template>
  <ul class="country__list">
    <li class="country__item" v-for="post in posts" :key="post">
      <router-link :to="{ name: 'CountryDetails', params: { id: post.cca3 } }">
        <div class="country__container">
          <img :src="post.flags.svg" alt="" />
          <p class="country__info"><span>Name:</span> {{ post.name.common }}</p>
          <p v-if="post.capital" class="country__info">
            <span>Capital:</span> {{ post.capital[0] }}
          </p>
          <p class="country__info">
            <span>Continent:</span> {{ post.continents[0] }}
          </p>
          <p class="country__info">
            <span>Population:</span> {{ post.population }}
          </p>
        </div>
      </router-link>
    </li>
  </ul>
</template>

<script setup>
defineProps({
  posts: {
    type: Array,
  },
});
</script>

<style scoped>

.country__list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}
.country__item {
  align-self: start;
  width: 25%;
  height: 500px;
  padding-bottom: 20px;
  border: 2px solid black;
  border-radius: 12px;
  margin-bottom: 30px;
  background: rgb(238, 174, 191);
  background: radial-gradient(
    circle,
    rgba(238, 174, 191, 1) 19%,
    rgba(148, 187, 233, 1) 74%
  );
}

.country__item + .country__item {
  margin-right: 10px;
}

.country__container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}
.country__info {
  align-self: self-start;
  margin-left: 15px;
  color: rgb(126, 13, 13);
}
.country__info span {
  font-weight: bold;
  font-size: 18px;
  color: black;
  text-transform: uppercase;
}
</style>

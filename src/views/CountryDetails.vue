<template>
  <div v-for="item in item" :key="item">
    <h2>{{ item.name.common }}</h2>
    <div class="item__container">
      <div class="item__about">
        <div class="item__names">
          <h3>Names</h3>
          <p><span>Common:</span> {{ item.name.common }}</p>
          <p><span>Ofiicial:</span> {{ item.name.official }}</p>
        </div>
        <div class="item__codes">
          <h3>Codes</h3>
          <p><span>ISO 3166-1 alpha-2:</span> {{ item.cca2 }}</p>
          <p><span>ISO 3166-1 alpha-3:</span> {{ item.cca3 }}</p>
          <p><span>ISO 3166-1 numeric:</span> {{ item.ccn3 }}</p>
          <p>
            <span>International calling code:</span> {{ item.idd.root
            }}{{ item.idd.suffixes[0] }}
          </p>
        </div>
        <div class="item__geography">
          <h3>Geography</h3>
          <p><span>Region:</span> {{ item.region }}</p>
          <p><span>Subegion:</span> {{ item.subregion }}</p>
          <p v-if="item.capital"><span>Capital:</span> {{ item.capital[0] }}</p>
          <p><span>Demonyms:</span> {{ item.demonyms.eng.f }}</p>
          <p><span>Area:</span> {{ item.area }} km</p>
        </div>
      </div>
      <div class="item__flag">
        <img :src="item.flags.png" alt="" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const props = defineProps({
  id: {
    type: String,
  },
});
const item = ref([]);
const error = ref(null);

onMounted(async () => {
  try {
    let data = await fetch(`https://restcountries.com/v3.1/alpha/${props.id}`);
    if (!data.ok) {
      throw Error("no data available");
    }
    item.value = await data.json();
  } catch (err) {
    error.value = err.message;
  }
  console.log(item.value);
});
</script>

<style scoped>
.item__container {
  display: flex;
  justify-content: space-between;
  margin-top: 30px;
}
.item__about {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  width: 50%;
}
.item__flag {
  width: 50%;
  margin-left: 100px;
}
.item__flag img {
  width: 500px;
}
.item__names,
.item__codes,
.item__geography {
  display: flex;
  flex-direction: column;
  border: 1px solid white;
  padding: 15px;
  border-radius: 4px;
  background: rgb(238, 174, 191);
  background: radial-gradient(
    circle,
    rgba(238, 174, 191, 1) 19%,
    rgba(148, 187, 233, 1) 74%
  );
}

p {
  color: rgb(78, 67, 67);
}
p + p {
  margin-top: 10px;
}
span {
  font-size: 18px;
  font-weight: bold;
  margin-right: 5px;
  color: rgb(3, 58, 58);
}
h2 {
    color: white;
  font-size: 60px;
}
h3 {
  color: rgb(3, 58, 58);
  font-size: 24px;
  margin-bottom: 15px;
}
</style>

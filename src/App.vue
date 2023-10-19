<template>
  <div>
    <header><h1>Country App</h1></header>
    <RouterView />
  </div>
</template>

<script setup>

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
header{
  border-bottom: 2px solid #dbbdbd;
  margin-bottom: 20px;
}
h1{
  margin-bottom: 20px;
  color: white;
  text-transform: uppercase;
  font-size: 36px;

}
</style>

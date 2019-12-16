<template>
  <button class="buttonPlay" @click="$emit('onClick')">Jogar</button>
</template>

<script>
export default {};
</script>

<style>
.buttonPlay {
  height: 35px;
  width: 80px;
  background-color: rgb(185, 167, 167);
  font-size: 1.2rem;
  border-radius: 5px;
}
</style>
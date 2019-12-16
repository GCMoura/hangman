<template>
  <button class="buttonNewPlay" @click="$emit('onClick')">Novo Jogo</button>
</template>

<script>
export default {};
</script>

<style>
.buttonNewPlay {
  height: 35px;
  width: 200px;
  background-color: rgb(185, 167, 167);
  font-size: 1.2rem;
  margin-top: 10px;
  border-radius: 5px;
}
</style>
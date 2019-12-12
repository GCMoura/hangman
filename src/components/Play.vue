<template>
<div>
    <input type="text" class="input" v-model="palavra">
    <button class="buttonPlay" @click="$emit('onClick', palavra)"> Jogar </button>
</div>
</template>

<script>
export default {
    props: {
        palavra: {}
  }
}
</script>

<style>
.input {
    height: 30px;
    width: 300px;
}

.buttonPlay {
    height: 35px;
    width: 80px;
    background-color: rgb(185, 167, 167);
    font-size: 1.2rem;
    margin-left: 10px;
}
</style>
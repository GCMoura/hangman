<template>
  <button class="button" @click="$emit('onClick', label)">
      {{ label }}
  </button>
</template>

<script>
export default {
    props: {
        label: {}        
    }
}
</script>

<style>
:root {
    --bg-button: rgb(185, 167, 167);
}

.button {
    width: 50px;
    height: 50px;
    font-size: 1.4em;
    background-color: var(--bg-button);
    border-radius: 50%;

}
</style>
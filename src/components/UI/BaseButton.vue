<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>

</script>

<style scoped>
button {
  cursor: pointer;
  font: inherit;
  background-color: #73adaf;
  border: 1px solid #124344;
  border-radius: 6px;
  color: white;
  padding: 0.5rem 2rem;
}
button:hover,
button:active {
background-color: #027a7e;
  border-color: #0c3334;
}
</style>
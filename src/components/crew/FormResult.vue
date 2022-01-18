<template>
  <div>
    <li>{{ name }}</li>
  </div>
</template>

<script>
export default {
  props: ['name'],
};
</script>

<style scoped>
li {
  padding: 0.25rem 0;
}
</style>
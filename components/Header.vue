<template>
  <div class="header">
    <div class="title">
      <h1>Qoala Test</h1>
    </div>
    <div class="button-container">
      <div class="button" @click="$emit('sort-by-color')">Color</div>
      <div class="button" @click="$emit('sort-by-city')">Cities</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Header"
};
</script>
<template>
  <select v-model="selected" class="select" multiple>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
</template>
<script>
export default {
  name: "my-multyselected",
};
</script>
<style scoped>
.select {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>
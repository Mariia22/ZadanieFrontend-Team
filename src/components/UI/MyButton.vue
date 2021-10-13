<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button",
};
</script>

<style scoped>
.btn {
  width: 150px;
  margin-top: 20px;
  margin-bottom: 20px;
  padding: 10px 15px;
  background: none;
  color: #6678b1;
  border: 1px solid #6678b1;
}
</style>
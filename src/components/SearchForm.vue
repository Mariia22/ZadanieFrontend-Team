<template>
  <form @submit.prevent>
    <my-input type="text" placeholder="Search..." />
    <my-multyselected :options="dzial" />
    <my-selected :options="kwota" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      dzial: ["IT", "B"],
      kwota: ["0-2000", "2000-4000", ">4000"],
    };
  },
  methods: {},
};
</script>

<style scoped>
form {
  display: flex;
  padding: 20px 50px 20px 20px;
}
</style>
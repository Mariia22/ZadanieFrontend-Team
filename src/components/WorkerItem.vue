<template>
  <tr>
    <th>{{ worker.imie }}</th>
    <th>{{ worker.nazwisko }}</th>
    <th>{{ worker.dzial }}</th>
    <th>{{ fullSalary }}</th>
  </tr>
</template>

<script>
export default {
  props: {
    worker: {
      type: Object,
      required: true,
    },
  },
  computed: {
    fullSalary: function () {
      return (
        this.worker.wynagrodzenieKwota + " " + this.worker.wynagrodzenieWaluta
      );
    },
  },
};
</script>

<style scoped>
</style>

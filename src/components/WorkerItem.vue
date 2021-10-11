<template>
  <tr>
    <td>{{ worker.imie }}</td>
    <td>{{ worker.nazwisko }}</td>
    <td>{{ worker.dzial }}</td>
    <td>{{ fullSalary }}</td>
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

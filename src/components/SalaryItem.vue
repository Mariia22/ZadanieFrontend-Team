<template>
  <tr>
    <th>{{ worker.dzial }}</th>
    <th>{{ sumSalaryDepartment }}</th>
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
    sumSalaryDepartment: function () {
      return this.worker.wynagrodzenieKwota;
    },
  },
};
</script>

<style scoped>
</style>

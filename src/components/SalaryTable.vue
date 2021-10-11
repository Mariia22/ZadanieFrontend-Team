<template>
  <div v-if="workers.length > 0">
    <table>
      <thead>
        <tr>
          <th>Dzial</th>
          <th>Suma wynagrodzenia</th>
        </tr>
      </thead>
      <tbody>
        <salary-item/>
      </tbody>
    </table>
   <div><strong>Suma całkowita</strong><p>{{}}</p></div>
  </div>
</template>

<script>
import SalaryItem from "@/components/SalaryItem.vue";

export default {
  components: {
    SalaryItem,
  },
  props: {
    workers: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
</style>
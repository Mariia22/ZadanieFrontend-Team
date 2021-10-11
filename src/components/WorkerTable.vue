<template>
  <div v-if="workers.length > 0">
    <table>
      <thead>
        <tr>
          <th>Imie</th>
          <th>Nazwisko</th>
          <th>Dzial</th>
          <th>Wynagrodzenie</th>
        </tr>
      </thead>
      <tbody>
        <worker-item
          v-for="worker in workers"
          :key="worker.index"
          :worker="worker"
        />
      </tbody>
    </table>
    <table>
      <thead>
        <tr>
          <th>Dzial</th>
          <th>Suma wynagrodzenia</th>
        </tr>
      </thead>
      <tbody>
        <salary-item :worker="worker" />
      </tbody>
      <tfoot>
        <tr>
          <td><strong>Suma całkowita</strong></td>
          <td>{{ sumSalary }}</td>
        </tr>
      </tfoot>
    </table>
  </div>
  <div v-else>
    <h1>Lista pracowników jest pusta</h1>
  </div>
</template>

<script>
import WorkerItem from "@/components/WorkerItem.vue";
//import SalaryItem from "@/components/WorkerItem.vue";

export default {
  components: {
    WorkerItem,
  },
  props: {
    workers: {
      type: Array,
      required: true,
    },
  },
  computed: {
    sumSalary: function calculateSum() {
      let sum = 0;
      this.workers.forEach((worker) => {
        sum += Number(worker.wynagrodzenieKwota);
      });
      console.log(sum);
      return sum;
    },
  },
};
</script>

<style>
</style>
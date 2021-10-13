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
    <div class="table_sum">
      <table>
        <thead>
          <tr>
            <th>Dzial</th>
            <th>Suma wynagrodzenia</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(value, key) in sumSalaryDepartments" :key="key">
            <td>{{ key }}</td>
            <td>{{ value }}</td>
          </tr>
        </tbody>
        <tfoot>
          <tr>
            <td><strong>Suma całkowita</strong></td>
            <td>{{ sumSalary }}</td>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
  <div v-else>
    <h1>Lista pracowników jest pusta</h1>
  </div>
</template>

<script>
import WorkerItem from "@/components/WorkerItem.vue";

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
      return sum;
    },
    sumSalaryDepartments: function calculateSumDepartments() {
      const departments = [];
      this.workers.forEach((worker) => {
        departments.push({
          key: worker.dzial,
          value: worker.wynagrodzenieKwota,
        });
      });
      const departmentsObject = departments.reduce(
        (acc, { key, value }) => (
          (acc[key] = (acc[key] || 0) + Number(value)), acc
        ),
        {}
      );
      return departmentsObject;
    },
  },
};
</script>

<style>
h1 {
  color: #6678b1;
}
.table {
  margin-top: 20px;
  border-collapse: collapse;
  font-size: 14px;
  background: white;
  text-align: left;
  font-size: 16px;
}
th {
  font-weight: normal;
  color: #039;
  border-bottom: 2px solid #6678b1;
  padding: 10px 8px;
}
td {
  color: #669;
  padding: 9px 8px;
  transition: 0.3s linear;
}
tr:hover td {
  color: #6699ff;
}
tr:nth-child(2n) {
  background: #e8edff;
}
.table_sum {
  display: flex;
  justify-content: right;
}
</style>
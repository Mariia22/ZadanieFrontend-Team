<template>
  <div id="app">
    <div>
      <form @submit.prevent>
        <my-input
          type="search"
          placeholder="Szukaj..."
          v-model="searchWorker"
        />
        <my-multyselected :options="dzial" />
        <my-selected
          :options="salary"
          :selection="selection"
          v-model="searchSalary"
        />
      </form>
      <my-button @click="showDialog"> Dodaj nowego pracownika </my-button>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <worker-form @create="createWorker" />
    </my-dialog>
    <worker-table :workers="sortedWorkersAndSalary" />
  </div>
</template>

<script>
import { persons, salaries } from "@/data.js";
import WorkerTable from "@/components/WorkerTable.vue";
import WorkerForm from "@/components/WorkerForm.vue";

export default {
  components: {
    WorkerTable,
    WorkerForm,
  },
  data() {
    return {
      workers: [],
      dialogVisible: false,
      dzial: ["IT", "B"],
      salary: [],
      selection: "kwotę wynagrodzenia",
      searchWorker: "",
      searchSalary: "",
    };
  },
  methods: {
    showDialog() {
      this.dialogVisible = true;
    },
    createWorker(worker) {
      this.workers.push(worker);
      this.dialogVisible = false;
    },
  },
  created() {
    this.workers = persons;
    this.salary = salaries;
  },
  computed: {
    sortedWorkers() {
      return this.workers.filter((worker) => {
        return (
          worker.imie.toLowerCase().includes(this.searchWorker.toLowerCase()) ||
          worker.nazwisko
            .toLowerCase()
            .includes(this.searchWorker.toLowerCase())
        );
      });
    },
    sortedWorkersAndSalary() {
      let begin, end;
      if (this.searchSalary === "0-2000") {
        begin = 0;
        end = 2000;
      } else if (this.searchSalary === "2001-3000") {
        begin = 2001;
        end = 3000;
      } else if (this.searchSalary === ">3000") {
        begin = 3001;
        end = Infinity;
      } else {
        begin = 0;
        end = Infinity;
      }
      return this.sortedWorkers.filter((worker) => {
        return (
          worker.wynagrodzenieKwota >= begin && worker.wynagrodzenieKwota <= end
        );
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
</style>

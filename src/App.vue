<template>
  <div id="app">
    <div class="wrapper">
      <form class="search_form" @submit.prevent>
        <my-input
          type="search"
          placeholder="Szukaj..."
          v-model="searchWorker"
        />
        <my-selected
          :options="salary"
          :selection="selection"
          v-model="searchSalary"
        />
        <select v-model="searchDepartment" class="search_multiselect" multiple>
          <option v-for="department in departments" :key="department">
            {{ department }}
          </option>
        </select>
      </form>
      <div class="workers">
        <my-dialog v-model:show="dialogVisible">
          <worker-form @create="createWorker" />
        </my-dialog>
        <h3>PRACOWNICY</h3>
        <worker-table :workers="sortedWorkersSalaryDepartment" class="table" />
        <my-button @click="showDialog"> + Dodaj nowego pracownika </my-button>
      </div>
    </div>
  </div>
</template>
//TODO: check sum to departments
//TODO: forms
<script>
import { persons, salaryData } from "@/data.js";
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
      departments: [],
      salary: [],
      selection: "kwotę wynagrodzenia",
      searchWorker: "",
      searchSalary: "",
      searchDepartment: [],
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
    this.salary = salaryData;
    this.departments = Array.from(
      new Set(
        [...this.workers].map((worker) => {
          return worker.dzial;
        })
      )
    );
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
      switch (this.searchSalary) {
        case "0-2000":
          begin = 0;
          end = 2000;
          break;
        case "2001-3000":
          begin = 2001;
          end = 3000;
          break;
        case ">3000":
          begin = 3001;
          end = Infinity;
          break;
        default:
          begin = 0;
          end = Infinity;
      }
      return this.sortedWorkers.filter((worker) => {
        return (
          worker.wynagrodzenieKwota >= begin && worker.wynagrodzenieKwota <= end
        );
      });
    },
    sortedWorkersSalaryDepartment() {
      const selectedDepartment = Object.values(this.searchDepartment);
      if (selectedDepartment.length > 0) {
        return this.sortedWorkersAndSalary.filter((worker) => {
          return selectedDepartment.includes(worker.dzial);
        });
      } else {
        return this.sortedWorkersAndSalary;
      }
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
h3 {
  margin: 0;
  color: #6678b1;
}
.wrapper {
  margin-top: 50px;
  display: flex;
  justify-content: center;
}
.search_form {
  margin: 47px 35px;
  display: flex;
  flex-direction: column;
}
.search_multiselect {
  width: 50%;
  border: 1px solid #6678b1;
  color: grey;
  margin: 15px 0;
}
</style>

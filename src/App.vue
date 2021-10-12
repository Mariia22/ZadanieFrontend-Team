<template>
  <div id="app">
    <div>
      <my-button @click="showDialog"> Dodaj nowego pracownika </my-button>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <worker-form @create="createWorker" />
    </my-dialog>
    <worker-table :workers="workers" />
  </div>
</template>

<script>
import WorkerTable from "@/components/WorkerTable.vue";
import WorkerForm from "@/components/WorkerForm.vue";

export default {
  components: {
    WorkerTable,
    WorkerForm,
  },
  data() {
    return {
      workers: [
        {
          imie: "Jan",
          nazwisko: "Kowalski",
          dzial: "IT",
          wynagrodzenieKwota: "3000",
          wynagrodzenieWaluta: "PLN",
        },
        {
          imie: "Anna",
          nazwisko: "Bąk",
          dzial: "Administracja",
          wynagrodzenieKwota: "2400.50",
          wynagrodzenieWaluta: "PLN",
        },
        {
          imie: "Paweł",
          nazwisko: "Zabłocki",
          dzial: "IT",
          wynagrodzenieKwota: "3300",
          wynagrodzenieWaluta: "PLN",
        },
        {
          imie: "Tomasz",
          nazwisko: "Osiecki",
          dzial: "Administracja",
          wynagrodzenieKwota: "2100",
          wynagrodzenieWaluta: "PLN",
        },
        {
          imie: "Iwona",
          nazwisko: "Leihs-Gutowska",
          dzial: "Handlowiec",
          wynagrodzenieKwota: "3100",
          wynagrodzenieWaluta: "PLN",
        },
      ],
      dialogVisible: false,
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

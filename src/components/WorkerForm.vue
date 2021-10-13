<template>
  <form @submit.prevent>
    <h4>Dane osobowe pracownika</h4>
    <my-input v-model="worker.imie" type="text" placeholder="Imie" />
    <my-input v-model="worker.nazwisko" type="text" placeholder="Nazwisko" />
    <my-selected
      v-model="worker.dzial"
      :options="department"
      :selection="selection[1]"
    />
    <my-input
      v-model="worker.wynagrodzenieKwota"
      type="number"
      placeholder="Wynagrodzenie"
    />
    <my-selected
      :options="currency"
      v-model="worker.wynagrodzenieWaluta"
      :selection="selection[0]"
    />
    <my-button @click="createWorker">Dodaj</my-button>
  </form>
</template>

<script>
import { currencyArr } from "@/data.js";
import { departmentArr } from "@/data.js";
export default {
  data() {
    return {
      worker: {
        imie: "",
        nazwisko: "",
        dzial: "",
        wynagrodzenieKwota: "",
        wynagrodzenieWaluta: "",
      },
      currency: [],
      department: [],
      selection: ["walutę", "dzial"],
    };
  },
  methods: {
    createWorker() {
      this.$emit("create", this.worker);
      this.worker = {
        imie: "",
        nazwisko: "",
        dzial: "",
        wynagrodzenieKwota: "",
        wynagrodzenieWaluta: "",
      };
    },
  },
  created() {
    this.currency = currencyArr;
    this.department = departmentArr;
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  padding: 2px 50px 2px 20px;
}
</style>
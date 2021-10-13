<template>
  <div class="form">
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
    </form>
    <my-button class="button" @click="createWorker">Dodaj</my-button>
  </div>
</template>

<script>
import { currencyData, departmentData } from "@/data.js";
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
    this.currency = currencyData;
    this.department = departmentData;
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}
form {
  display: flex;
  flex-direction: column;
  padding: 2px 30px 2px 20px;
}
h4 {
  margin: 10px;
  color: #6678b1;
}
.button {
  align-items: center;
}
</style>
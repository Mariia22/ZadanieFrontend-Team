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
    <div class="error">
    <p v-if="errors.length">
  <b>Proszę poprawić następujące błędy &#128533;</b>
  <ul>
    <li v-for="error in errors" :key="error">{{ error }}</li>
  </ul>
</p>
</div>
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
      errors: [],
      currency: [],
      department: [],
      selection: ["walutę", "dzial"],
    };
  },
  methods: {
    createWorker() {
      this.errors = [];
      if (
        this.worker.imie &&
        this.worker.nazwisko &&
        this.worker.dzial &&
        this.worker.wynagrodzenieKwota &&
        this.worker.wynagrodzenieWaluta
      ) {
        this.$emit("create", this.worker);

        this.worker = {
          imie: "",
          nazwisko: "",
          dzial: "",
          wynagrodzenieKwota: "",
          wynagrodzenieWaluta: "",
        };
      } else {
        if (!this.worker.imie) this.errors.push("Imie wymagane");
        if (!this.worker.nazwisko) this.errors.push("Nazwisko rwymagane");
        if (!this.worker.dzial) this.errors.push("Dzial wymagane");
        if (!this.worker.wynagrodzenieKwota)
          this.errors.push("Wynagrodzenie wymagane");
        if (!this.worker.wynagrodzenieWaluta)
          this.errors.push("Waluta wymagane");
      }
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
.error {
  color: #6678b1;
}
</style>
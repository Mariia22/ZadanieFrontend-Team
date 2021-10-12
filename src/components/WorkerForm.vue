<template>
  <form @submit.prevent>
    <h4>Dane osobowe pracownika</h4>
    <my-input v-model="worker.imie" type="text" placeholder="Imie" />
    <my-input v-model="worker.nazwisko" type="text" placeholder="Nazwisko" />
    <my-input v-model="worker.dzial" type="text" placeholder="Dzial" />
    <my-input
      v-model="worker.wynagrodzenieKwota"
      type="number"
      placeholder="Wynagrodzenie"
    />
    <my-selected :options="currency" v-model="worker.wynagrodzenieWaluta" />
    <my-button @click="createWorker">Dodaj</my-button>
  </form>
</template>

<script>
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
      currency: ["PLN", "EUR", "USD"],
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
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  padding: 2px 50px 2px 20px;
}
</style>
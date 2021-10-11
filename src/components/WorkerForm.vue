<template>
  <form @submit.prevent>
    <h4>Dane osobowe pracownika</h4>
    <my-input type="text" placeholder="Imie" />
    <my-input type="text" placeholder="Nazwisko" />
    <my-input type="text" placeholder="Dzial" />
    <my-input type="number" placeholder="Wynagrodzenie" />
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
      },
    };
  },
  methods: {
    createWorker() {
      console.log(1);
      /*   this.$emit("create", this.worker);
      this.worker = {
        imie: "",
        nazwisko: "",
        dzial: "",
        wynagrodzenieKwota: "",
      }; */
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  padding: 50px;
}
</style>
<template>
  <div>
    <table-pracownicy />
  </div>
</template>

<script>
import TablePracownicy from "@/components/TablePracownicy.vue";

export default {
  name: "App",
  components: {
    TablePracownicy,
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

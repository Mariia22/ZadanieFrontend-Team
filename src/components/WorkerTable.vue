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
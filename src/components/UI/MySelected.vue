<template>
  <select :value="modelValue" @input="updateSelect" class="select">
    <option :selected="true" value="" disabled>
      Proszę wybrać {{ selection }}
    </option>
    <option
      v-for="option in options"
      :key="option"
      :selected="option === modelValue"
    >
      {{ option }}
    </option>
  </select>
</template>

<script>
export default {
  name: "my-selected",
  props: {
    options: {
      type: Array,
      required: true,
    },
    label: {
      type: String,
      default: "",
    },
    modelValue: String,
    selection: [String, Array],
  },
  methods: {
    updateSelect(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style scoped>
.select {
  border: 1px solid #6678b1;
  padding: 2px 5px;
  margin: 15px 0;
  color: grey;
}
</style>

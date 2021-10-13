<template>
  <div>
    <label v-if="label">{{ label }}</label>
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
  </div>
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
    selection: String,
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
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>

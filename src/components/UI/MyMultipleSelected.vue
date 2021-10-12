<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <select
      :value="modelValue"
      @input="updateMultiSelect"
      class="select"
      multiple
    >
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
  name: "my-multyselected",
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
  },
  methods: {
    updateMultiSelect(event) {
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
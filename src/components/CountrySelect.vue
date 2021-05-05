<template>
  <select
    @change="onChange"
    v-model="selected"
    class="form-select bg-gray-300 bg-opacity-25 block w-full border p-3 rounded mt-10"
  >
    <option value="0">select</option>
    <option v-for="country in countries" :key="country.ID" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected);
      this.$emit("get-country", country);
    },
  },
};
</script>

<style></style>

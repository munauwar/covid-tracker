<template>
  <select
    @change="onChange()"
    v-model="selected"
    class="form-select mt-10 mb-5 block w-full border p-3 rounded"
  >
    <option value="0">Select Country</option>
    <option v-for="countryName in countries" :key="countryName.ID" :value="countryName.ID">
      {{ countryName.Country }}
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
      console.log(country);

      this.$emit("getCountry", country);
    },
  },
};
</script>
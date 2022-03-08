<template>
  <select
    @change="onChange()"
    v-model="selected"
    class="mt-10 mb-5 block w-4/5 border p-3 rounded mx-auto"
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

      this.$emit("getCountry", country);
    },
  },
};
</script>
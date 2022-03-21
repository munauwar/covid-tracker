<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <CountrySelect @getCountry="getCountryData" :countries="countries" />
    <DataBoxes :stats="stats" />
    <Graphs :data="dataGraph" class="w-1/2 mx-auto"/>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="" />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";
import Graphs from "@/components/Graphs.vue"

export default {
  name: "HomeView",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
    Graphs
  },
  data() {
    return {
      loading: true,
      title: "Global cases",
      dataDate: "",
      stats: {},
      countries: [],
      dataGraph: [{ 
        barName1: "Total Deaths",
        barValue1: 0,
        barName2: "Total confirmed cases",
        barValue2: 0,
      }],
      loadingImage: require("../assets/timer.gif"),
    };
  },
  methods: {
    async fetchApiData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },

    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
      this.dataGraph = [{
        barName1: "Total Deaths", 
        barValue1: country.TotalDeaths,
        barName2: "Total confirmed cases",
        barValue2: country.TotalConfirmed
      }];
    },
  },
  async created() {
    const data = await this.fetchApiData();

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.dataGraph.barValue1 = data.Global.TotalDeaths;
    this.dataGraph.barValue2 = data.Countries.TotalConfirmed;
    this.loading = false;
  },
};
</script>

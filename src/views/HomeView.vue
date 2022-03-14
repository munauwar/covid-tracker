<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <CountrySelect @getCountry="getCountryData" :countries="countries" />
    <DataBoxes :stats="stats" />
    <Graphs :data="data"/>
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
import moment from 'moment'

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
      data: [{ name: 'Jan', pl: 1000 }],
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
    },
  },
  async created() {
    const data = await this.fetchApiData();

    this.data = data.Countries.map(item => {
        name: moment(item.Date).format("MMMM");
        pl: item.NewDeaths;
    }) 

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.deaths = data.TotalDeaths;
    this.loading = false;
  },
};
</script>

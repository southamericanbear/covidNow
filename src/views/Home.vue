<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelect :countries="countries" @get-country="getCountryData" />
    <button
      v-if="stats.Country"
      @click="clearCountryData"
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
    >
      Clear Country
    </button>

    <CountryDataBox
      v-if="countrySelected"
      :country="country"
      :countryFlag="countryFlag"
    />
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-grey-500 text-3xl mt-10 mb6">Fetching Data</div>
    <img :src="loadingImage" class="w-24 m-auto" alt="loading" />
  </main>
</template>

<script>
import DataTitle from "../components/DataTitle";
import DataBoxes from "../components/DataBoxes";
import CountrySelect from "../components/CountrySelect";
import CountryDataBox from "../components/CountryDataBox";

export default {
  name: "Home",
  components: { DataTitle, DataBoxes, CountrySelect, CountryDataBox },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/tenor.gif"),
      country: {},
      countryCode: "",
      countryFlag: "",
      countrySelected: false,
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },

    getCountryData(country) {
      this.stats = country;
      this.country = country;
      this.title = country.Country;
      let countryCodeUpper = country.CountryCode;
      this.countryCode = countryCodeUpper.toLowerCase();
      this.countryFlag = `https://flagcdn.com/h240/${this.countryCode}.png `;
      this.countrySelected = true;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = "Global";
      this.stats = data.Global;
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>

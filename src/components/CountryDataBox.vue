<template>
  <div class="box flex flex-col justify-around md:flex-row my-10">
    <div class="left">
      <img class="w-50" :src="countryFlag" :alt="country" />
      <Map :country="country" />
    </div>
    <div class="right">
      <h1>{{ country.Country }}</h1>
      <span
        >Total Confirmed: {{ numberWithCommas(country.TotalConfirmed) }}</span
      >
      <br />
      <span>New Cases: {{ numberWithCommas(country.NewConfirmed) }}</span>
      <br />
      <span>Total Deaths: {{ numberWithCommas(country.TotalDeaths) }}</span>
      <br />
      <span>New Deaths: {{ numberWithCommas(country.NewDeaths) }}</span>
    </div>
  </div>
</template>

<script>
import Map from "./Map";

export default {
  name: "CountryDataBox",
  props: ["country", "countryFlag"],
  components: { Map },
  methods: {
    numberWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    },
  },
};
</script>

<style>
.box {
  border: solid 2px red;
}
</style>

<template>
  <div ref="mapDiv">{{ latitud }} {{ longitud }}</div>
</template>

<script>
/* eslint-disable no-undef */

export default {
  name: "Map",
  props: ["country"],
  data() {
    return {
      latitud: "",
      longitud: "",
    };
  },
  methods: {
    async fetchCountryLatLng() {
      const res = await fetch(
        `https://api.covid19api.com/country/${this.country.Country}`
      );
      const data = await res.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchCountryLatLng();
    this.latitud = data[0].Lat;
    this.longitud = data[0].Lon;
  },
};
</script>

<style scoped>
div {
  border: solid 2px blue;
}
</style>

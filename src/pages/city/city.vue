<template>
  <div>
    <city-header></city-header>
    <city-search :cities="cities"></city-search>
    <city-list :cities="cities"  :hot="hotCities" :letter="letter"></city-list>
    <city-aiphabet :cities="cities" @change="handleLetterChange"></city-aiphabet>
  </div>
</template>

<script>
  import CityHeader from "./components/Header";
  import CitySearch from "./components/Search";
  import CityList from "./components/List";
  import CityAiphabet from "./components/Aiphabet";
  import axios from "axios";
  export default {
    name: "City",
    components: {
      CityHeader,
      CitySearch,
      CityList,
      CityAiphabet
    },
    data() {
      return {
        cities: {},
        hotCities: [],
        letter:''
      };
    },
    methods: {
      getCityInfo() {
        axios.get("/api/city.json").then(res => {
          console.log(res);
          var res= res.data;
          if(res.data){
              this.cities= res.data.cities;
              this.hotCities = res.data.hotCities;
          }
        });
      },
      handleLetterChange(letter){
          console.log(letter)
          this.letter= letter
      }
    },
    mounted() {
      this.getCityInfo();
    }
  };
</script>

<style lang="scss" scoped></style>

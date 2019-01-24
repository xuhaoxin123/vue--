<template>
          <div>
              <city-header></city-header>
              <city-search></city-search>
              <city-list></city-list>
              <city-aiphabet></city-aiphabet>
          </div>

</template>


<script>

import CityHeader from "./components/Header";
import CitySearch from "./components/Search";
import CityList from "./components/List";
import CityAiphabet from "./components/Aiphabet";
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

      };
    }
  };
</script>

<style lang="scss" scoped>


</style>


<template>
  <div class="container">
    <Header/>
    <div id="sections-wrapper">
      <div class="covid-wrapper">
        <search-country @country-value="getCountryInput"></search-country>
        <country-data :countrySelectedPass="countrySelected"></country-data>
      </div>
      <country-data id="italian-data" class="covid-wrapper" :countrySelectedPass="'Italy'"></country-data>
    </div>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import SearchCountry from './components/UI/SearchCountry.vue';
import CountryData from './components/UI/CountryData.vue';

export default {
  name: 'App',
  components: {
    Header, SearchCountry,CountryData
  },
  data() {
    return { 
      countrySelected: '',
    }
  },
  methods: {
    getCountryInput(val) {
      this.countrySelected = val;
    }
  }
}
</script>

<style lang="scss">
* {
  @import url('https://fonts.googleapis.com/css2?family=Lato:wght@100;300;400;700&display=swap');
  font-family: 'Lato', sans-serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  background-color:#DFDFDF;
}

.container {
  width: 80%;
  margin: 0 auto;
}

#sections-wrapper {
    content: "";
    display: table;
    clear: both;
    width: 100%;
    margin: auto;

  .covid-wrapper {
    float: left;
    width: 35%;
  }

  #italian-data.covid-wrapper {
    float: right;
    margin-top: 20px;
  }
}


</style>

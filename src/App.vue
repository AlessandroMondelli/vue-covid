<template>
  <div class="container">
    <Header/>
    <div id="sections-wrapper">
      <div class="covid-wrapper">
        <search-country @country-value="getCountryInput"></search-country>
      </div>
       <div class="covid-wrapper">
        <country-data :countrySelectedPass="countrySelected"></country-data>
      </div>
    </div>
    <div id="container-logo">
      <img id="logo-covid" :src="require('@/assets/covid19.png')" alt="covid logo">
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
  background-color:#292626;
  color: white;
}

body {
  max-height: 95vh;
  max-width: 100vw;
  overflow: hidden;
}

.container {
  width: 80%;
  margin: 0 auto;
}

#sections-wrapper {
    height: 55vh;
    display: flex;
    align-items: center;

  .covid-wrapper {
    margin-left: 10%;
  }
}


#container-logo {
    position: absolute;
    filter: grayscale(100%);
    transition: 1s;
    overflow: hidden;

    &:hover {
      filter: grayscale(0);
    }

    img {
      position: absolute;
      height: 100%;
    }
  }

$breakpoint-smartphone: 320px;
$breakpoint-tablet: 767px;
$breakpoint-laptop: 992px;
$breakpoint-large: 1200px;

@media (min-width: $breakpoint-smartphone) {
  #sections-wrapper {
    align-items: center;
    flex-wrap: wrap;
  }

  #container-logo {
    height: 100px;
    width: 100px;
    bottom: -10%;
    right: 0;
  }
}

@media (min-width: $breakpoint-tablet) {
  #container-logo {
    height: 150px;
    bottom: -10%;
    right: 0;
  }
}

@media (min-width: $breakpoint-laptop) {
  #container-logo {
    height: 300px;
    bottom: -25%;
    right: 0;
  }
}

@media (min-width: $breakpoint-large) {
  #container-logo {
    height: 300px;
    bottom: -15%;
    right: 0%;
  }
}

</style>

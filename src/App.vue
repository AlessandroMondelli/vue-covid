<template>
  <div class="container">
    <Header/>
    <italian-data/> 
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';
import ItalianData from './components/UI/ItalianData.vue';

export default {
  name: 'App',
  components: {
    Header, ItalianData
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

</style>

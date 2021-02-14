<template>
  <div id="app">
    <div class="title">
          <h1>Covid Tracker Vue.js</h1>
    </div>
    <div class="cards animate__animated ">
      <Confirmed :selected="selected"/>
      <Recovered :selected="selected"/>
      <Dead :selected="selected"/>
    </div>
    <div class="dropdown animate__animated">
      <b-form-select v-model="selected" v-on:change="changeCountry()">
            <template #first>
                <b-form-select-option :value="null" disabled>
                    -- Please select a country --
                </b-form-select-option>
            </template>

            <b-form-select-option v-for="(country, i) in countries" :key="i" :value="country.name">{{country.name}}</b-form-select-option>
        </b-form-select>
    </div>
  </div>
</template>

<script>
import Confirmed from './components/Confirmed';
import Dead from './components/Dead';
import Recovered from './components/Recovered';

import axios from 'axios';

export default {
  name: 'App',
  components: {
    Confirmed,
    Dead,
    Recovered,
  },

  data() {
    return {
      countries: '',
      selected: null,
    }
  },

  mounted() {
    document.querySelector(".cards").classList.add("animate__zoomIn");

    this.countryRequest();
  },

  methods: {
    countryRequest() {
            axios
                .get('https://covid19.mathdro.id/api/countries')
                .then(response => this.countries = response.data.countries);
    },

    changeCountry() {
        this.selected = event.target.value;
    },
  }
}
</script>

<style lang="scss"> 
  #app {
    height: 100vh;
    background-color: rgb(255, 255, 180);
  }

  .title {
    height: 100px;
    border-bottom: 2px solid rgba(0, 60, 255, 0.612);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .cards {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    column-gap: 20px;
    width: 90%;
    margin: auto;
    margin-top: 50px;
  }

  .dropdown {
    margin: auto;
    margin-top: 75px;
    max-width: 500px;
  }

</style>

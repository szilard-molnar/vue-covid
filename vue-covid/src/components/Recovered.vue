<template>
    <div id="covid-recovered">
        <div class="covid-card">
            <div class="covid-card-header">
                <p>Recovered</p>
            </div>
            <div class="covid-card-body">
                <p>Number of Recovered:<br><strong>{{addCommasToNumber()}}</strong></p>
                <p>As of<br><strong>{{date | moment("dddd, MMMM Do YYYY")}}</strong></p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return{
            covid: '',
            date: '',
        }
    },

    methods: {
        addCommasToNumber() {
            return this.covid.toLocaleString();
        }
    },

    mounted() {
        axios
            .get('https://covid19.mathdro.id/api')
            .then(response => {
                this.covid = response.data.recovered.value;
                this.date = response.data.lastUpdate;
            })
            .catch(error => console.log(error));
    }
}
</script>

<style lang="scss">
    #covid-recovered .covid-card {
        max-width: 275px;
        height: 300px;
        background-color: white;
        text-align: center;
        border-radius: 20px;
        box-shadow: 0px 0px 20px 0px rgb(0, 181, 15);
    }

    #covid-recovered .covid-card-header {
        padding: 25px 20px;
        background-color: rgba(4, 33, 252, 0.345);
        border-radius: 20px 20px 0 0;
    }

    #covid-recovered .covid-card-header p {
        margin-bottom: 0;
        font-size: 28px;
        font-weight: 700;
    }

    #covid-recovered .covid-card-body {
        padding: 10px 20px;
        display: grid;
        align-items: center;
        height: 200px;
    }

    #covid-recovered .covid-card-body p {
        margin-bottom: 0;
    }
</style>
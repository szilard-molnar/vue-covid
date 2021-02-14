<template>
    <div id="covid-confirmed">
        <div class="covid-card">
            <div class="covid-card-header">
                <p>Confirmed</p>
            </div>
            <div class="covid-card-body">
                <p>Confirmed number: {{covid}}</p>
                <p>As of {{date}}</p>
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

    },

    mounted() {
        axios
            .get('https://covid19.mathdro.id/api')
            .then(response => {
                this.covid = response.data.confirmed.value;
                this.date = response.data.lastUpdate;
            })
            .catch(error => console.log(error))
    }
}
</script>

<style lang="scss">
    .covid-card {
        max-width: 300px;
        background-color: white;
        text-align: center
    }
</style>
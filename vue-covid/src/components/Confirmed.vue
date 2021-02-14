<template>
    <div id="covid-confirmed">
        <div class="covid-card">
            <div class="covid-card-header">
                <p>Confirmed</p>
            </div>
            <div class="covid-card-body">
                <p>Confirmed number</p>
                <p>{{covid}}</p>
                <!-- <p>As of {{info.data.lastUpdate}}</p> -->
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
        }
    },

    methods: {

    },

    mounted() {
        axios
            .get('https://covid19.mathdro.id/api')
            .then(response => (this.covid = response))
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
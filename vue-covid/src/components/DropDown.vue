<template>
    <div id="dropdown">
        
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            countries: '',
        }
    },

    mounted() {
        this.countryRequest();
    },

    methods: {
        countryRequest() {
            axios
                .get('https://covid19.mathdro.id/api/countries')
                .then(response => this.countries = response.data.countries);
        },
    }
}
</script>

<style lang="scss">
    #dropdown {
        height: fit-content;
    }
</style>
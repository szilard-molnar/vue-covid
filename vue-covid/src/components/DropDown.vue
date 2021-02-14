<template>
    <div id="dropdown">
        <b-form-select v-model="selected">
            <template #first>
                <b-form-select-option :value="null" disabled>
                    -- Please select an option --
                </b-form-select-option>
            </template>

            <b-form-select-option v-for="(country, i) in countries" :key="i">{{country.name}}</b-form-select-option>
        </b-form-select>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            countries: '',
            selected: null,
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
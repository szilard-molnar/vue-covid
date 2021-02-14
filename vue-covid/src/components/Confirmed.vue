<template>
    <div id="covid-confirmed">
        <div class="covid-card" @mouseenter="mouseEnter()" @mouseleave="mouseLeave()">
            <div id="confirmed-overlay" class="animate__animated "></div>
            <div class="covid-card-header">
                <p>Confirmed</p>
            </div>
            <div class="covid-card-body">
                <p>Number of Confirmed:<br><strong>{{addCommasToNumber()}}</strong></p>
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
        },

        mouseEnter() {
            if(document.getElementById("confirmed-overlay").classList.contains("animate__fadeIn"))
            {
                document.getElementById("confirmed-overlay").classList.remove("animate__fadeIn");
                document.getElementById("confirmed-overlay").classList.add("animate__fadeOut");
            }
            else 
            {
                document.getElementById("confirmed-overlay").classList.add("animate__fadeOut");
            }
            setTimeout(function(){
                this.showThis = false;
            }, 750);
        },

        mouseLeave() {
            if(document.getElementById("confirmed-overlay").classList.contains("animate__fadeOut"))
            {
                document.getElementById("confirmed-overlay").classList.remove("animate__fadeOut");
                document.getElementById("confirmed-overlay").classList.add("animate__fadeIn");
            }
            this.showThis = true;
        }
    },

    mounted() {
        axios
            .get('https://covid19.mathdro.id/api')
            .then(response => {
                this.covid = response.data.confirmed.value;
                this.date = response.data.lastUpdate;
            })
            .catch(error => console.log(error));
    }
}
</script>

<style lang="scss">
    #covid-confirmed {
        margin: auto;
    }

    #covid-confirmed #confirmed-overlay {
        height: 100%;
        width: 100%;
        background-color: rgba(0, 0, 198, 0.201);
        z-index: 9999;
        border-radius: 20px;
        position: absolute;
    }

    #covid-confirmed .covid-card {
        position: relative;
        max-width: 275px;
        height: 300px;
        background-color: white;
        text-align: center;
        border-radius: 20px;
        box-shadow: 0px 0px 35px 0px rgba(13, 23, 96, 0.63);
    }

    #covid-confirmed .covid-card-header {
        padding: 25px 20px;
        background-color: rgba(4, 33, 252, 0.345);
        border-radius: 20px 20px 0 0;
    }

    #covid-confirmed .covid-card-header p {
        margin-bottom: 0;
        font-size: 28px;
        font-weight: 700;
    }

    #covid-confirmed .covid-card-body {
        padding: 10px 20px;
        display: grid;
        align-items: center;
        height: 200px;
    }

    #covid-confirmed .covid-card-body p {
        margin-bottom: 0;
    }
</style>
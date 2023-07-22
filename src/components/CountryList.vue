<template>
    <h2>Current Speaker</h2>
    <div class="currentSpeaker">
        <img :src="currentSpeaker.imageSrc" height="44" class="countryFlag">
        <h1 class="countryName">{{ currentSpeaker.officialName }}</h1>
    </div>
    <div id="upcomingSpeakers">
        <h2>Upcoming Speakers</h2>
    <div id="countryList">
        <div v-for="country in upcomingSpeakers" :key="country" class="countryInList">
            <img height="46" :src="country.imageSrc" class="countryFlag">
            <h3 class="countryName">{{ country.officialName }}</h3>
        </div>
    </div>
    </div>
    <button>Add Speaker</button>
</template>
<script>
    export default {
        data() {
            return {

            }
        },
        props: {
            propList: Array
        },
        computed: {
            currentSpeaker() {
                return this.propList[0]
            },
            upcomingSpeakers() {
                return this.propList.slice(1)
            }
        }
    }
</script>
<style>
    .countryName {
        display: inline-block;
        margin: 0;
        padding: 10px;
        vertical-align: middle;
    }
    .countryFlag {
        vertical-align: middle;
    }
    .countryInList {
        vertical-align: middle;
        text-align: left;
    }
    #countryList {
        display:inline-block;
    }
    #upcomingSpeakers {
        margin-bottom: 20px;
    }
</style>
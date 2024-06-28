<template>

    <body>
        <div class="picture-search">
            <h1> <strong>Welcome weary traveler and behold, as teh marvels unfold</strong> </h1>


            <div v-if="state.loaded">
                <PictureCard :pictureData="state.pictureData" />
            </div>
            <div class='no-data' v-else>
                <div class="toggleToSearch">
                    <button type="button" @click="getPictureData">Fetch me a picture of the day!</button>
                </div>
                No picture here yet, Oh no 😢
            </div>

        </div>
    </body>


</template>
<script>
import axios from "axios"
import { reactive } from 'vue'
import PictureCard from "./PictureCard.vue";

axios.defaults.headers['X-API-KEY'] = 'api_key_here';


export default {
    components: { PictureCard },
    setup() {

        const state = reactive({
            loaded: false,
            todayDate: '',
            pictureData: '',
        })

        function getPictureData() {
            state.todayDate = getCurrentDate()
            getPictures()
        }

        function getCurrentDate() {
            let currentDate = new Date().toJSON().slice(0, 10);
            return currentDate;

        }

        function getPictures() {
            axios.get(`api/apod?date=${state.todayDate}`)
                .then(response => {
                    state.pictureData = response.data
                    state.loaded = true
                })
                .catch(err => {
                    console.error(err);
                });

        }

        return {
            state,
            getPictureData
        }

    }
}
</script>

<style scoped>
.picture-container h1 {
    color: #8B008B;
}

.toggleToSearch {
    font-family: Verdana, sans-serif;
}

.no-data {
    color: #6b5f6b;
}
</style>
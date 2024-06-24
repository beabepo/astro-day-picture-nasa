<template>

    <body>
        <div class="picture-search">
            <h1> <strong>Welcome weary traveler and behold, as teh marvels unfold</strong> </h1>
            <div class="toggleToSearch">
                <button type="button" @click="getPictureData">Fetch me a picture of the day!</button>
            </div>

            <div v-if="state.loaded">
                <div class="picture-data">
                    <h1><strong>{{ state.pictureData.title }}</strong></h1>
                    <p>Date: {{ state.pictureData.date }}</p>
                    <img :src="state.pictureData.url" alt="Normal picture no hd">
                    <p v-if="state.pictureData.copyright">Copyright:{{ state.pictureData.copyright }}</p>
                    <p>
                        <a :href="state.pictureData.hdurl" target="_blank">Hd version of teh picta</a>
                    </p>
                    <div class="picture-explanation"> Description: {{ state.pictureData.explanation }}</div>

                </div>
            </div>
            <div v-else>No picture here, Oh no 😢 </div>

        </div>
    </body>


</template>
<script>
import axios from "axios"
import { reactive } from 'vue'

axios.defaults.headers['X-API-KEY'] = 'your_API_key_here_;P';


export default {
    components: {},
    setup() {

        const state = reactive({
            loaded: false,
            todayDate: '2024-06-20',
            pictureData: '',
        })

        function getPictureData() {
            getPictures()
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
.picture-data h1 {
    color: #8B008B;
}

.toggleToSearch {
    font-family: Verdana, sans-serif;
}
</style>
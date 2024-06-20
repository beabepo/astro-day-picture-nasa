<template>

    <body>
        <div class="picture-search">
            <h1> Welcome weary traveller and behold, as teh marvels unfold </h1>
            <div class="toggleToSearch">
                <button type="button" @click="getPictureData">Fetch me a picture of the day!</button>
            </div>

            <div v-if="state.loaded"> {{ state.pictureData }}
            </div>
            <div v-else>No picture here, Oh no 😢 </div>

        </div>
    </body>


</template>
<script>
import axios from "axios"
import { reactive } from 'vue'

axios.defaults.headers['X-API-KEY'] = 'key_here_:D';


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
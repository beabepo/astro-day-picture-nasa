<template>

    <body>
        <div class="picture-search">
            <h1> Welcome weary traveller and behold, as teh marvels unfold </h1>
            <div class="toggleToSearch">
                <button type="button" @click="getPictureData">Fetch me a picture of the day!</button>
            </div>

            <div v-if="state.loaded">
            </div>
            <div v-else>No picture here, Oh no 😢 </div>

        </div>
    </body>


</template>
<script>
import axios from "axios"
import { ref, reactive } from 'vue'

const getPicture = ref('')

export default {
    components: {},
    setup() {

        const state = reactive({
            loaded: false,
            pictureData: '',
        })

        return {
            state
        }

    }
}
</script>
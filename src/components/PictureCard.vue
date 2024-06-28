<template>
    <div class="card-container">
        <div class="card-wrapper">
            <div class="picture-header"> <strong>{{ pictureData.title }} </strong></div>
            <div class="picture-data"></div>
            <p>Today's Date: {{ pictureData.date }}</p>
            <div class="images-data">
                <img :src="pictureData.url" alt="Normal picture no hd">
                <p v-if="pictureData.copyright">Copyright:{{ pictureData.copyright }}</p>
                <p>
                    <a :href="pictureData.hdurl" target="_blank">Hd version of the Picture</a>
                </p>
            </div>
            <div class="picture-explanation"> Description: {{ pictureData.explanation }}</div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'PictureCard',

    props: ['pictureData'],
};

</script>

<style scoped></style>
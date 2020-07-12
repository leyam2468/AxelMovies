<template>
    <div class="bannerImg">
        <div
            class="Imgbox"
            :style="{
                Background:
                    'url(https://image.tmdb.org/t/p/w780/w2uGvCpMtvRqZg6waC1hvLyZoJa.jpg)',
                BackgroundSize: 'cover',
                BackgroundRepeat: 'no-repeat',
                Width: '100%',
                Height: '500px',
                BackgroundPosition: 'center center',
            }"
        >
            <img
                :src="`https://image.tmdb.org/t/p/w780${video.backdrop_path}`"
                alt=""
                width="100px"
                height="400px"
            />
        </div>
    </div>
</template>

<script>
export default {
    props: {
        video: {
            type: Object,
            default: null,
        },
    },
}
</script>

<style>
.bannerImg .imgbox img {
    width: 200px;
}
</style>

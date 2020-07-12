<template>
    <div>
        <v-img
            :src="`https://image.tmdb.org/t/p/w500${video.poster_path}`"
            class="grey lighten-2 elevation-20"
            max-width="300"
            max-height="400"
        >
            <div class="video-card-info">
                <v-row justify="center" align="center" class="pa-3">
                    <h2 class="color-one font-weight-black">
                        {{ video.original_title | shorten(40) }}
                    </h2>
                    <v-divider class="py-2"></v-divider>
                    <p>{{ video.overview | shorten(110) }}</p>

                    <v-rating
                        v-model="video.vote_average"
                        background-color="red lighten-3"
                        color="red"
                        length="10"
                    ></v-rating
                ></v-row>
            </div>
        </v-img>
    </div>
</template>

<script>
export default {
    filters: {
        shorten(v, num) {
            if (v.length > num) {
                return v.substring(0, num) + ' .....'
            } else {
                return v
            }
        },
    },
    props: {
        video: {
            type: Object,
            default: null,
        },
    },
}
</script>

<style lang="scss" scoped>
.video-card-info {
    background-color: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
    opacity: 0;

    transition: opacity 0.5s ease-in-out;
    &:hover {
        opacity: 1;
    }
}
</style>

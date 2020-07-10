<template>
    <div class="banner">
        <v-carousel
            continuous
            cycle
            height="400"
            hide-delimiter-background
            show-arrows-on-hover
            delimiter-icon="mdi-minus"
        >
            <v-carousel-item
                v-for="video in videos"
                :key="video.id"
                :src="`https://image.tmdb.org/t/p/w780${video.backdrop_path}`"
                reverse-transition="fade-transition"
                transition="fade-transition"
            >
                <v-sheet color="rgba(30, 30, 30, 0.5)" height="100%" tile>
                    <v-row class="fill-height" align="center" justify="center">
                        <v-col md="4" cols="12"
                            ><v-row class="" align="center" justify="center">
                                <v-img
                                    :src="`https://image.tmdb.org/t/p/w500${video.poster_path}`"
                                    aspect-ratio="1"
                                    class="grey lighten-2 elevation-20"
                                    max-width="300"
                                    max-height="300"
                                >
                                </v-img> </v-row
                        ></v-col>
                        <v-col md="8" class="hidden-xs-only"
                            ><div class="pa-10">
                                <h2
                                    class="color-one font-weight-black display-3"
                                >
                                    {{ video.original_title | shorten(40) }}
                                </h2>
                                <v-divider class="py-2"></v-divider>
                                <p>{{ video.overview | shorten(450) }}</p>

                                <v-rating
                                    v-model="video.vote_average"
                                    background-color="red lighten-3"
                                    color="red"
                                    length="10"
                                ></v-rating></div
                        ></v-col>
                    </v-row> </v-sheet
            ></v-carousel-item>
        </v-carousel>
        <div v-for="video in videos" :key="video.id">
            {{ video }}<v-divider class="py-2"></v-divider>
        </div>
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
        videos: {
            type: Array,
            default: null,
        },
    },
    data() {
        return {
            src: 'https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg',
            items: [
                {
                    src:
                        'https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg',
                },
                {
                    src: 'https://cdn.vuetifyjs.com/images/carousel/sky.jpg',
                },
                {
                    src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg',
                },
                {
                    src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg',
                },
            ],
        }
    },
}
</script>

<style></style>

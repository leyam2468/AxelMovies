<template>
    <div class="BannerSlide">
        <div
            :style="{
                BackgroundImage: `url(https://image.tmdb.org/t/p/w780${video.backdrop_path})`,
            }"
            class="BannerBox"
        >
            <v-sheet color="rgba(30, 30, 30, 0.5)" height="100%" tile>
                <v-container>
                    <v-row
                        class="fill-height h-100"
                        align="center"
                        justify="center"
                    >
                        <v-col md="4" cols="12">
                            <v-img
                                :src="`https://image.tmdb.org/t/p/w500${video.poster_path}`"
                                class="grey lighten-2 elevation-20"
                                max-width="300"
                                max-height="400"
                            >
                            </v-img>
                        </v-col>
                        <v-col md="8" class="hidden-xs-only"
                            ><div class="pa-2">
                                <h2
                                    class="color-one font-weight-black display-3"
                                >
                                    {{
                                        video.original_title ||
                                        video.title ||
                                        video.original_name ||
                                        video.name | shorten(35)
                                    }}
                                </h2>
                                <v-divider class="py-2"></v-divider>
                                <p>{{ video.overview | shorten(250) }}</p>

                                <v-rating
                                    v-model="video.vote_average"
                                    background-color="red lighten-3"
                                    color="red"
                                    length="10"
                                ></v-rating></div
                        ></v-col>
                    </v-row>
                </v-container>
            </v-sheet>
        </div>
    </div>
</template>

<script>
export default {
    filters: {
        shorten(v, num) {
            if (v.length > num) {
                return v.substring(0, num) + ' .....'
            } else if (v === undefined) {
                return 'no title'
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

<style lang="scss">
.BannerSlide {
    width: 100%;
    height: 450px;
    .BannerBox {
        width: 100%;
        height: 100%;
        background-size: cover;
        background-position: center center;
    }
}
</style>

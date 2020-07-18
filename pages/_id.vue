<template>
    <div class="video">
        <div
            :style="{
                BackgroundImage: `url(https://image.tmdb.org/t/p/original${video.backdrop_path})`,
            }"
            class="BannerBox elevation-20"
        >
            <!-- Banner Sheet Info -->
            <v-sheet color="rgba(30, 30, 30, 0.5)" height="100%" tile>
                <v-container>
                    <v-row
                        class="fill-height h-100"
                        align="center"
                        justify="center"
                    >
                        <!-- Img  -->
                        <v-col md="4" cols="12">
                            <v-img
                                :src="`https://image.tmdb.org/t/p/w500${video.poster_path}`"
                                class="grey lighten-2 elevation-20"
                                max-width="300"
                                max-height="400"
                            >
                            </v-img>
                        </v-col>
                        <!-- Info Movie -->
                        <v-col md="8" class="hidden-xs-only"
                            ><div class="pa-2">
                                <!-- title -->
                                <h2
                                    class="color-one font-weight-black display-3"
                                >
                                    {{
                                        video.original_title ||
                                        video.title ||
                                        video.original_name ||
                                        video.name
                                    }}
                                </h2>
                                <!--  -->
                                <v-divider class="py-2"></v-divider>
                                <!-- overlay -->
                                <p class="white--text">
                                    {{ video.overview }}
                                </p>
                                <!-- Rating -->
                                <v-rating
                                    v-model="video.vote_average"
                                    background-color="yellow accent-3"
                                    color="yellow"
                                    length="10"
                                ></v-rating>
                                <!--  -->
                                <div class="my-1">
                                    <v-btn
                                        class="ma-1"
                                        color="black white--text"
                                        >{{ video.popularity }}
                                        <v-icon color="yellow accent-3" right
                                            >mdi-eye</v-icon
                                        >
                                    </v-btn>
                                    <v-btn
                                        class="ma-2"
                                        color="black white--text"
                                        >{{ video.vote_average }}/10
                                        <v-icon color="yellow accent-3" right
                                            >mdi-star</v-icon
                                        >
                                    </v-btn>
                                </div>
                                <!-- Genre -->
                                <div>
                                    <v-btn color="black white--text ma-2">{{
                                        video.release_date
                                    }}</v-btn>
                                    <v-btn color="black white--text ma-2">{{
                                        video.production_countries[0].name
                                    }}</v-btn>
                                    <v-btn color="black white--text ma-2">{{
                                        video.spoken_languages[0].name
                                    }}</v-btn>
                                </div>
                                <div>
                                    <v-btn
                                        v-for="genre in video.genres"
                                        :key="genre.id"
                                        color="black white--text ma-2"
                                        >{{ genre.name }}</v-btn
                                    >
                                </div>
                                <v-btn
                                    to="/video"
                                    class="mt-3"
                                    color="red white--text"
                                    >See Movie</v-btn
                                >
                            </div>
                        </v-col>
                    </v-row>
                    <v-divider class="mb-1"></v-divider>
                    <v-divider class="mb-3"></v-divider>
                    <v-row>
                        <v-col v-for="vid in youtube" :key="vid.id">
                            <iframe
                                width="250"
                                height="250"
                                :src="`https://www.youtube.com/watch?v=${vid.id}`"
                                frameborder="0"
                                allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
                                allowfullscreen
                            ></iframe>
                        </v-col>
                    </v-row>
                </v-container>
            </v-sheet>
        </div>
    </div>
</template>

<script>
export default {
    async asyncData({ $axios, error, params }) {
        try {
            const video = await $axios.get(
                `https://api.themoviedb.org/3/movie/${params.id}?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US`
            )
            const youtube = await $axios.get(
                'https://api.themoviedb.org/3/movie/299534/videos?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US'
            )
            // console.log(video)
            return {
                video: video.data,
                youtube: youtube.data.results,
            }
        } catch (e) {
            error({
                statusCode: 503,
                maessage: 'Cant Get vidos, please try angine',
            })
        }
    },
}
</script>

<style lang="scss" scoped>
.video {
    width: 100%;
    height: 100%;
    .BannerBox {
        width: 100%;
        height: 100%;
        background-attachment: fixed;
        background-size: cover;
        background-position: center center;
    }
}
</style>

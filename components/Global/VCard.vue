<template>
    <div>
        <v-img
            :src="`https://image.tmdb.org/t/p/w500${video.poster_path}`"
            class="grey lighten-2 elevation-20"
            width="300"
            height="400"
        >
            <div class="video-card-info">
                <!-- title -->
                <h3 class="color-one font-weight-black">
                    {{
                        video.original_title ||
                        video.title ||
                        video.original_name ||
                        video.name
                    }}
                </h3>

                <v-divider class="my-2"></v-divider>
                <!-- <p class="white--text">{{ video.overview | shorten(100) }}</p> -->

                <!-- Rating -->
                <v-rating
                    v-model="rating"
                    background-color="yellow accent-3"
                    color="yellow "
                    length="5"
                    class="mt-1"
                ></v-rating>
                <!--  -->
                <div class="my-1">
                    <v-btn class="ma-1" color="black white--text"
                        >{{ video.popularity }}
                        <v-icon color="yellow accent-3" right>mdi-eye</v-icon>
                    </v-btn>
                    <v-btn class="ma-2" color="black white--text"
                        >{{ video.vote_average }}/10
                        <v-icon color="yellow accent-3" right>mdi-star</v-icon>
                    </v-btn>
                </div>

                <!-- Catagre -->
                <div class="my-1">
                    <v-btn
                        v-for="genre_id in video.genre_ids.slice(0, 2)"
                        :key="genre_id.id"
                        class=""
                        color="black white--text"
                    >
                        <span v-for="genre in genres" :key="genre.id">
                            <span v-if="genre_id == genre.id" class="">{{
                                genre.name
                            }}</span>
                        </span>
                        <v-icon color="yellow accent-3" right
                            >mdi-checkbox-marked-circle</v-icon
                        >
                    </v-btn>
                </div>

                <!-- BTN  See More -->
                <div>
                    <v-btn
                        :to="'/' + video.id"
                        class="mt-3"
                        color="red white--text"
                        >See Movie</v-btn
                    >
                </div>
            </div>
        </v-img>
    </div>
</template>

<script>
export default {
    // filters: {
    //     shorten(v, num) {
    //         if (v.length > num) {
    //             return v.substring(0, num) + ' .....'
    //         } else {
    //             return v
    //         }
    //     },
    // },
    props: {
        video: {
            type: Object,
            default: null,
        },
        genres: {
            type: Array,
            default: null,
        },
    },
    data() {
        return {
            rating: this.video.vote_average / 2,
        }
    },
}
</script>

<style lang="scss" scoped>
.video-card-info {
    background-color: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
    opacity: 0;
    text-align: center;
    padding: 10px;

    transition: opacity 0.5s ease-in-out;
    &:hover {
        opacity: 1;
    }
}
</style>

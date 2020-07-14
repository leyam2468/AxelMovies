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
                <h2 class="color-one font-weight-black">
                    {{ video.original_title | shorten(100) }}
                </h2>

                <v-divider class="py-2"></v-divider>
                <p class="white--text">{{ video.overview | shorten(100) }}</p>
                <!-- Rating -->
                <v-rating
                    v-model="rating"
                    background-color="red lighten-1"
                    color="red"
                    length="5"
                ></v-rating>
                <!-- Catagre -->
                <span
                    v-for="genre_id in video.genre_ids"
                    :key="genre_id.id"
                    class="pa-2 ma-3 color-one font-weight-black"
                >
                    <span v-for="genre in genres" :key="genre.id">
                        <span v-if="genre_id == genre.id">{{
                            genre.name
                        }}</span>
                    </span>
                </span>
                <!-- BTN  See More -->
                <div>
                    <v-btn to="/video" class="mt-3" color="red white--text"
                        >See Movie</v-btn
                    >
                </div>
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

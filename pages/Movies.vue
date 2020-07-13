<template>
    <div class="Movies">
        <h1>Movies</h1>
        <v-row no-gutters="">
            <v-col
                v-for="video in movie.results"
                :key="video.id"
                cols="6"
                md="3"
            >
                <VCard :video="video" />
            </v-col>
        </v-row>
        <div class="text-center my-5">
            <v-pagination
                v-model="page"
                :length="movie.total_pages"
                total-visible="15"
                prev-icon="mdi-menu-left"
                next-icon="mdi-menu-right"
            ></v-pagination>
            {{ page }}
        </div>
    </div>
</template>

<script>
import VCard from '@/components/Global/VCard'

export default {
    components: {
        VCard,
    },
    async asyncData({ $axios, error }) {
        try {
            const movie = await $axios.get(
                'https://api.themoviedb.org/3/movie/top_rated?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US&page=1'
            )
            console.log(movie)
            return {
                movie: movie.data,
            }
        } catch (e) {
            error({
                statusCode: 503,
                maessage: 'Cant Get vidos, please try angine',
            })
        }
    },
    data() {
        return {
            page: 1,
        }
    },
}
</script>

<style></style>

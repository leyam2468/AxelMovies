<template>
    <div class="Movies">
        <div class="title my-5 ml-3">
            <h1>Movies</h1>
        </div>
        <!--  -->
        <v-row dense justify="center" align="center">
            <v-col v-for="video in posts" :key="video.id" cols="6" md="2">
                <VCard :video="video" :genres="genres" />
            </v-col>
        </v-row>
        <!--  -->
        <v-pagination
            v-model="page"
            :length="totalPages"
            total-visible="15"
            class="my-5"
            color="red"
            @input="next"
        ></v-pagination>
    </div>
</template>

<script>
import VCard from '@/components/Global/VCard'

export default {
    components: {
        VCard,
    },
    watchQuery: ['page'],
    async asyncData({ $axios, error, query }) {
        try {
            const page = query.page || 1
            const movie = await $axios.get(
                'https://api.themoviedb.org/3/movie/top_rated?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US&page=' +
                    page
            )
            const genres = await $axios.get(
                'https://api.themoviedb.org/3/genre/movie/list?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US'
            )
            console.log(movie)
            return {
                posts: movie.data.results,
                page: movie.data.page,
                totalPages: movie.data.total_pages,
                genres: genres.data.genres,
            }
        } catch (e) {
            error({
                statusCode: 503,
                maessage: 'Cant Get vidos, please try angine',
            })
        }
    },
    methods: {
        next() {
            this.$router.push({ query: { page: this.page } })
        },
    },
}
</script>

<style>
.title {
    padding: 5px 10px;
    border-left: 3px solid red;
}
</style>

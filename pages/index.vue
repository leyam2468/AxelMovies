<template>
    <div class="home">
        <v-container>
            <!-- Last News -->
            <LastNews />
            <!-- Banner -->
            <VueSlickCarousel v-bind="BannerSlickOptions">
                <BannerSlide
                    v-for="video in trendingAll"
                    :key="video.id"
                    :video="video"
                />
            </VueSlickCarousel>
        </v-container>

        <!-- Trending -->
        <div class="trending">
            <div class="title my-5 ml-3">
                <h1 class="d-inline-block">Trinding Movies</h1>
                <v-btn text class="watcheBTN">Watche All</v-btn>
            </div>
            <VueSlickCarousel v-bind="slickOptions">
                <div v-for="video in videos" :key="video.id">
                    <VCard :video="video" :genres="genres" />
                </div>
            </VueSlickCarousel>
        </div>

        <!-- Puplare -->
        <div class="puplare">
            <div class="title my-5 ml-3">
                <h1 class="d-inline-block">Top Rated Movies</h1>
                <v-btn text class="watcheBTN">Watche All</v-btn>
            </div>
            <VueSlickCarousel v-bind="slickOptions">
                <div v-for="video in movie" :key="video.id">
                    <VCard :video="video" :genres="genres" />
                </div>
            </VueSlickCarousel>
        </div>
    </div>
</template>

<script>
import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
// optional style for arrows & dots
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'
import LastNews from '@/components/Home/LastNews'
import BannerSlide from '@/components/Global/BannerSlide'
import VCard from '@/components/Global/VCard'

export default {
    components: {
        LastNews,
        BannerSlide,
        VCard,

        VueSlickCarousel,
    },
    async asyncData({ $axios, error }) {
        try {
            // Trinding Movie Day
            const trendingAll = await $axios.get(
                'https://api.themoviedb.org/3/trending/all/day?api_key=e248b861c3ca5e9cf5bb0113718abaf2'
            )
            // Trinding Movie Day
            const trendingMovieDay = await $axios.get(
                'https://api.themoviedb.org/3/trending/movie/day?api_key=e248b861c3ca5e9cf5bb0113718abaf2'
            )
            // Movies Top Rated
            const movie = await $axios.get(
                'https://api.themoviedb.org/3/movie/top_rated?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US&page=1'
            )
            // Catagre Movies
            const genres = await $axios.get(
                'https://api.themoviedb.org/3/genre/movie/list?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US'
            )
            console.log(trendingAll.data.results)
            return {
                trendingAll: trendingAll.data.results,
                videos: trendingMovieDay.data.results,
                movie: movie.data.results,
                genres: genres.data.genres,
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
            slickOptions: {
                slidesToShow: 5,
                arrows: false,
                autoplay: true,
                autoplaySpeed: 3000,
                focusOnSelect: false,
                responsive: [
                    {
                        breakpoint: 750,
                        settings: {
                            slidesToShow: 2,
                            slidesToScroll: 2,
                        },
                    },
                ],
            },
            BannerSlickOptions: {
                arrows: false,
                slidesToShow: 1,
                autoplay: true,
                autoplaySpeed: 3000,
            },
        }
    },
    head() {
        return {
            title: 'Home Page',
        }
    },
}
</script>
<style lang="scss">
.title {
    padding: 5px 10px;
    border-left: 3px solid red;
    .watcheBTN {
        color: red;
        font-weight: bold;
    }
}
</style>

<template>
    <div class="home">
        <v-container>
            <!-- Last News -->
            <LastNews />
            <!-- Banner -->
            <VueSlickCarousel v-bind="BannerSlickOptions">
                <BannerSlide
                    v-for="video in videos"
                    :key="video.id"
                    :video="video"
                />
            </VueSlickCarousel>
        </v-container>

        <!-- Trending -->
        <div class="trending">
            <VueSlickCarousel v-bind="slickOptions">
                <div v-for="video in videos" :key="video.id">
                    <VCard :video="video" />
                </div>
            </VueSlickCarousel>
        </div>
        <!-- Puplare -->
        <div class="puplare">
            <h1>Puplare Movies</h1>
            <VueSlickCarousel v-bind="slickOptions">
                <div v-for="video in movie" :key="video.id">
                    <VCard :video="video" />
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
            const trending = await $axios.get(
                'https://api.themoviedb.org/3/trending/movie/day?api_key=e248b861c3ca5e9cf5bb0113718abaf2'
            )

            const movie = await $axios.get(
                'https://api.themoviedb.org/3/movie/top_rated?api_key=e248b861c3ca5e9cf5bb0113718abaf2&language=en-US&page=1'
            )
            return {
                videos: trending.data.results,
                movie: movie.data.results,
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
                arrows: true,
                autoplay: true,
                autoplaySpeed: 3000,
                focusOnSelect: false,
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
<style lang="scss"></style>

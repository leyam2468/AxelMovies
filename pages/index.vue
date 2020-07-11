<template>
    <div class="home">
        <v-container>
            <LastNews />
            <banner :videos="videos" />
        </v-container>
        <div>
            <VueSlickCarousel v-bind="slickOptions">
                <div v-for="video in videos" :key="video.id">
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
import banner from '@/components/Home/banner'
import VCard from '@/components/Global/VCard'

export default {
    components: {
        LastNews,
        banner,
        VCard,
        VueSlickCarousel,
    },
    async asyncData({ $axios, error }) {
        try {
            const { data } = await $axios.get(
                'https://api.themoviedb.org/3/trending/movie/day?api_key=e248b861c3ca5e9cf5bb0113718abaf2'
            )
            return {
                videos: data.results,
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
                autoplaySpeed: 1000,
                focusOnSelect: false,
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
<style lang="scss" scoped></style>

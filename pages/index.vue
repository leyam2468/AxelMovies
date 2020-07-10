<template>
    <div class="home">
        <v-container>
            <LastNews />
            <banner :videos="videos" />
        </v-container>
    </div>
</template>

<script>
import LastNews from '@/components/Home/LastNews'
import banner from '@/components/Home/banner'
export default {
    components: {
        LastNews,
        banner,
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
    head() {
        return {
            title: 'Home Page',
        }
    },
}
</script>

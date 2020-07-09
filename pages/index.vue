<template>
    <div class="home">
        <v-container>
            <LastNews />
            <banner />
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
}
</script>

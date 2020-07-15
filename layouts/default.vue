<template>
    <v-app dark>
        <Navbar />
        <v-main>
            <nuxt />
        </v-main>
        <Fotter />
    </v-app>
</template>

<script>
import Navbar from '@/components/Global/Navbar.vue'
import Fotter from '@/components/Global/Fotter.vue'
export default {
    data() {
        return {}
    },
    component: {
        Navbar,
        Fotter,
    },
}
</script>

<template>
    <v-app dark>
        <Navbar />
        <v-main>
            <nuxt />
        </v-main>
    </v-app>
</template>

<script>
import Navbar from '@/components/Global/Navbar.vue'
export default {
    data() {
        return {
            clipped: false,
            drawer: false,
            fixed: false,
            items: [
                {
                    icon: 'mdi-apps',
                    title: 'Welcome',
                    to: '/',
                },
                {
                    icon: 'mdi-chart-bubble',
                    title: 'Inspire',
                    to: '/inspire',
                },
            ],
            miniVariant: false,
            right: true,
            rightDrawer: false,
            title: 'Vuetify.js',
        }
    },
    component: {
        Navbar,
    },
}
</script>

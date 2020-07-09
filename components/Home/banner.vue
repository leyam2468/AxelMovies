<template>
    <div class="banner">
        <v-carousel
            continuous
            cycle
            height="400"
            hide-delimiter-background
            show-arrows-on-hover
            delimiter-icon="mdi-minus"
        >
            <v-carousel-item
                v-for="(item, i) in items"
                :key="i"
                :src="item.src"
                reverse-transition="fade-transition"
                transition="fade-transition"
            >
                <v-sheet color="#1e1e1e59" height="100%" tile>
                    <v-row class="fill-height" align="center" justify="center">
                        <v-col
                            ><div class="display-3">
                                Slide {{ i + 1 }}
                            </div></v-col
                        >
                        <v-col
                            ><div class="display-3">
                                Slide {{ i + 1 }}
                            </div></v-col
                        >
                    </v-row>
                </v-sheet></v-carousel-item
            >
        </v-carousel>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [
                {
                    src:
                        'https://cdn.vuetifyjs.com/images/carousel/squirrel.jpg',
                },
                {
                    src: 'https://cdn.vuetifyjs.com/images/carousel/sky.jpg',
                },
                {
                    src: 'https://cdn.vuetifyjs.com/images/carousel/bird.jpg',
                },
                {
                    src: 'https://cdn.vuetifyjs.com/images/carousel/planet.jpg',
                },
            ],
        }
    },
}
</script>

<style></style>

<template>
    <div>
        <!-- SideBar -->
        <v-navigation-drawer v-model="siteNav" color="colorOne" fixed temporary>
            <!-- Links -->
            <v-list dense nav class="py-2">
                <v-list-item two-line>
                    <v-list-item-avatar>
                        <img
                            src="https://randomuser.me/api/portraits/men/81.jpg"
                        />
                    </v-list-item-avatar>

                    <v-list-item-content>
                        <v-list-item-title>Mohamed Ahmed</v-list-item-title>
                        <v-list-item-subtitle>Wep Design</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>

                <v-divider></v-divider>
                <v-list-item v-for="link in links" :key="link.to">
                    <v-btn text class="font-weight-bold" nuxt :to="link.to">
                        {{ link.title }}
                    </v-btn>
                </v-list-item>
            </v-list>
            <!-- buttom Section -->
            <template v-slot:append>
                <div class="pa-2">
                    <v-btn block elevation="8">Login</v-btn>
                </div>
            </template>
        </v-navigation-drawer>

        <!-- NavBar -->
        <v-app-bar hide-on-scroll app class="navbar-area" height="50px">
            <v-app-bar-nav-icon
                class="hidden-sm-and-up"
                @click.stop="siteNav = !siteNav"
            ></v-app-bar-nav-icon>
            <!-- title logo -->
            <v-toolbar-title class="font-weight-bold text-uppercase font-one">
                <nuxt-link
                    to="/"
                    :class="[darktheme ? 'black--text' : 'white--text']"
                    >Axel<span class="color-one">4</span>Movies</nuxt-link
                >
            </v-toolbar-title>
            <!-- Search -->
            <v-spacer></v-spacer>

            <!-- <v-toolbar-items>
                <v-autocomplete
                    v-model="model"
                    :items="items"
                    :loading="isLoading"
                    :search-input.sync="search"
                    color="white"
                    class="pt-1"
                    hide-no-data
                    hide-selected
                    item-text="Description"
                    item-value="API"
                    placeholder="Search"
                    prepend-icon="mdi-database-search"
                    return-object
                ></v-autocomplete>
            </v-toolbar-items> -->

            <v-spacer></v-spacer>
            <!-- links -->
            <v-toolbar-items class="hidden-xs-only">
                <v-btn
                    v-for="link in links"
                    :key="link.title"
                    text
                    class="font-weight-bold"
                    nuxt
                    :to="link.to"
                >
                    {{ link.title }}
                </v-btn>
            </v-toolbar-items>
            <!-- icons links -->
            <v-toolbar-items>
                <!-- dark -->
                <v-btn icon @click="toggletheme">
                    <v-icon>
                        mdi-{{
                            `${darktheme ? 'weather-night' : 'brightness-6'}`
                        }}</v-icon
                    >
                </v-btn>
                <v-btn icon>
                    <v-icon>mdi-movie-search-outline</v-icon>
                </v-btn>
                <!-- Setting -->
                <!-- <v-dialog
                    v-model="dialog"
                    fullscreen
                    hide-overlay
                    transition="dialog-bottom-transition"
                >
                    <template v-slot:activator="{ on, attrs }">
                        <v-btn text v-bind="attrs" v-on="on"
                            ><v-icon>mdi-cog</v-icon></v-btn
                        >
                    </template>
                    <v-card>
                        <v-toolbar>
                            <v-toolbar-title>Settings</v-toolbar-title>
                            <v-spacer></v-spacer>
                            <v-btn @click="dialog = false"
                                ><v-icon>mdi-close</v-icon></v-btn
                            >
                        </v-toolbar>
                    </v-card>
                </v-dialog> -->
            </v-toolbar-items>
        </v-app-bar>
    </div>
</template>

<script>
export default {
    components: {},
    data() {
        return {
            descriptionLimit: 60,
            entries: [],
            isLoading: false,
            model: null,
            search: null,
            //
            dialog: false,
            siteNav: false,
            darktheme: false,
            // src: require('~/assets/logo2.png'),
            links: [
                {
                    to: '/',
                    title: 'Home',
                    icon: 'mdi-apps',
                },
                {
                    to: 'trending',
                    title: 'Trending',
                    icon: 'mdi-cast-education',
                },
                {
                    to: 'tv',
                    title: 'TV Show',
                    icon: 'mdi-solar-panel-large',
                },
                {
                    to: 'movies',
                    title: 'Movies',
                    icon: 'mdi-account-cash',
                },
                {
                    to: 'Popular',
                    title: 'Popular',
                    icon: 'mdi-card-account-mail',
                },
                {
                    to: 'Lastadd',
                    title: 'Last Added',
                    icon: 'mdi-account-alert',
                },
            ],
        }
    },
    computed: {
        fields() {
            if (!this.model) return []

            return Object.keys(this.model).map((key) => {
                return {
                    key,
                    value: this.model[key] || 'n/a',
                }
            })
        },
        items() {
            return this.entries.map((entry) => {
                const Description =
                    entry.Description.length > this.descriptionLimit
                        ? entry.Description.slice(0, this.descriptionLimit) +
                          '...'
                        : entry.Description

                return Object.assign({}, entry, { Description })
            })
        },
    },

    watch: {
        search(val) {
            // Items have already been loaded
            if (this.items.length > 0) return

            // Items have already been requested
            if (this.isLoading) return

            this.isLoading = true

            // Lazily load input items
            fetch('https://api.publicapis.org/entries')
                .then((res) => res.json())
                .then((res) => {
                    const { count, entries } = res
                    this.count = count
                    this.entries = entries
                })
                .catch((err) => {
                    console.log(err)
                })
                .finally(() => (this.isLoading = false))
        },
    },
    methods: {
        toggletheme() {
            this.$vuetify.theme.dark = !this.$vuetify.theme.dark
            this.darktheme = !this.darktheme
        },
    },
}
</script>

<style lang="scss" scoped></style>

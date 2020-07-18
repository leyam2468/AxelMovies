<template>
    <v-app dark>
        <h1 v-if="error.statusCode === 404">
            {{ pageNotFound }}
        </h1>
        <h1 v-else>
            {{ otherError }}
        </h1>
        <NuxtLink to="/">
            Home page
        </NuxtLink>
    </v-app>
</template>

<script>
export default {
    layout: 'empty',
    props: {
        error: {
            type: Object,
            default: null,
        },
    },
    data() {
        return {
            pageNotFound: '404 Not Found',
            otherError: 'An error occurred',
        }
    },
    head() {
        const title =
            this.error.statusCode === 404 ? this.pageNotFound : this.otherError
        return {
            title,
        }
    },
}
</script>

<style scoped>
h1 {
    font-size: 5rem;
    font-weight: bold;
    text-align: center;
    color: red;
}
a {
    width: 200px;
    margin: 0 auto;
    text-align: center;
    padding: 10px;
    color: red;
    background-color: white;
    border-radius: 4px;
    transition: all 0.5s ease-in-out;
}
a:hover {
    color: white;
    background-color: red;
}
</style>

<template>
    <div class="lastnews">
        <marquee
            behavior=""
            direction="right"
            class="grey darken-3 white--text lastnews-text color-one"
            >This Site Is Under Develop, please Wait Completing Data</marquee
        >
        <span>
            Last News
        </span>
    </div>
</template>

<script>
export default {}
</script>

<style scoped>
.lastnews-text {
    border-radius: 5px;
    padding: 5px 0;
    position: relative;
}
span {
    position: absolute;
    width: 100px;
    padding: 5px;
    background-color: red;
    border-radius: 5px;
    right: 50px;
    text-align: center;
    color: white;
}
</style>

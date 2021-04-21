<template>
    <section id="header">
        <h1>Covid-19 Stats</h1>
        <img :src="require('@/assets/covid19.png')" alt="covid logo">
    </section>
</template>

<script>
export default {
    name: "Header"
}
</script>

<style lang="scss" scoped>
    #header {
        height: 80px;
        line-height: 80px;
        margin: 30px 0 50px;

        h1 {
            font-size: 32px;
            display: inline-block;
        }

        img {
            display: inline-block;
            width: 50px;
            vertical-align: middle;
            margin: 0 0 12px 15px;
        }
    }

    $breakpoint-smartphone: 320px;
    $breakpoint-tablet: 767px;
    $breakpoint-laptop: 992px;
    $breakpoint-large: 1200px;

    @media (min-width: $breakpoint-smartphone) {
        #header {
            h1 {
                font-size: 24px;
            }
        }
        
    }
</style>
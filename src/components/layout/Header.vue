<template>
    <section id="header">
        <h1>Covid-19 Stats</h1>
        <img :src="require('@/assets/covid19.png')">
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
        margin-top: 30px;

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
</style>
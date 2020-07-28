<template>
    <div class="skill-chart">
        <div class="skill">{{text}}</div>
        <div class="chart">
            <div v-for="index in 10" :key="index" class="gray-dot">
                <div ref="blue" class="blue-dot"></div>
            </div>
        </div>
    </div>
</template>

<script>
    import gsap from "gsap"
    import { ScrollTrigger } from "gsap/ScrollTrigger"

    gsap.registerPlugin(ScrollTrigger);
    export default {
        mounted () {
            const dots = this.$refs.blue.slice(0, this.number);
            const tl = gsap.timeline({
                scrollTrigger: {
                    trigger: '.other-skills'
                }
            })

            tl.to(dots, {opacity: 1, stagger: {each: .8}, delay: 1})

        },
        props: {
            text: {
                type: String 
            },
            number: {
                type: Number 
            },
        },
    }
</script>

<style lang="stylus" scoped>
    .skill-chart
        display flex
        padding 15px 0
        flex-wrap wrap
        justify-content space-between
        .skill
            min-width 120px
            padding-bottom 10px
        .chart
            display flex
            justify-content space-between
            flex-basis 70%
            padding-right 30px
            max-width 400px
            .gray-dot
                position relative
                height 20px
                width 20px
                background-color #61616130
                border-radius 20px
                .blue-dot
                    width 100%
                    height 100%
                    background-color var(--background-third-color)
                    border-radius 20px
                    opacity 0
</style>
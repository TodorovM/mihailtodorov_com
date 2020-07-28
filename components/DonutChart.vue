<template>
    <div class="donut">
        <svg width='200' height='200' class="lower-circle" ref="lower">
            <circle cx="100" cy="100" r="90" stroke="#61616130" stroke-width="15"  fill="transparent" />
        </svg>
        <svg width='200' height='200' class="upper-circle" ref="upper">
            <circle cx="100" cy="100" r="90" stroke="#1f4068" stroke-width="15"  stroke-linecap="round" fill="transparent" />
        </svg>
        <span ref="text">{{ text }}</span>
    </div>
</template>

<script>
    import gsap from "gsap"
    import { ScrollTrigger } from "gsap/ScrollTrigger"

    gsap.registerPlugin(ScrollTrigger);
    export default {
        computed: {
            dash() {
                return (this.dashArray / 100) * (2 * Math.PI * 90)
            }
        },
        props: {
            dashArray: {
                type: Number, 
            },
            text: {
                type: String
            }
        },
        mounted () {
            const lower = this.$refs.lower;
            const upper = this.$refs.upper;
            const text = this.$refs.text;
            const tl = gsap.timeline({
                scrollTrigger: {
                    trigger: '#skills'
                }
            })

            tl
              .to(lower, {duration: 1, strokeDashoffset: 0, delay: 1})
              .to(upper, {duration: 1, strokeDashoffset: "0"})
              .to(upper, {duration: 1, strokeDasharray: this.dash})
              .to(text, {duration: 1, opacity:1})
        },
    }
</script>

<style lang="stylus" scoped>
    .donut
        width 200px
        height 200px
        position relative;
        margin 20px
        svg 
            stroke-dashoffset 1000
            stroke-dasharray 1000
        .upper-circle
            position absolute
            top 0
            left 0
            transform rotate(90deg)
    span 
        position absolute
        top 50%
        left 50%
        transform translateX(-50%) translateY(-50%)
        opacity 0
</style>
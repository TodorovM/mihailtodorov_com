<template>
    <div class="work-example" ref="example">
        <div class="example-image" ref="exampleImage"></div>
        <div class="btn-container">
            <a v-if="example.github" :href="example.github" class="github">GitHub</a>
            <a v-if="example.link" :href="example.link" class="link">Link</a>
        </div>
    </div>
</template>

<script>
    import gsap from 'gsap'
    export default {
        props: {
            example: {
                type: Object
            },
        },
        methods: {
            hoverAnimation(e) {
                const maxDeg = 16;
                const dimensions = {
                    width: e.target.getBoundingClientRect().width,
                    height: e.target.getBoundingClientRect().height
                }
                const angleRatio = {
                    x: maxDeg / (dimensions.width / 2),
                    y: maxDeg / (dimensions.height / 2)
                }

                const angle = {
                    x: angleRatio.x * (dimensions.width / 2 - e.offsetX),
                    y: angleRatio.y * (dimensions.height / 2 - e.offsetY) * -1
                }

                gsap.to(this.$refs.example, {duration: .5, rotateY: `${angle.x}deg`, rotateX: `${angle.y}deg`})
            },
            hoverOut(e) {
                gsap.to(this.$refs.example, {duration: .5, rotateX: "0deg", rotateY: "0deg"})
            }
        },
        mounted () {
           this.$refs.exampleImage.style.backgroundImage = `url(${require(`../assets/${this.example.image}`)})` ;
           this.$refs.exampleImage.addEventListener('mousemove', this.hoverAnimation);
           this.$refs.exampleImage.addEventListener('mouseout', this.hoverOut)
        },
    }
</script>

<style lang="stylus" scoped>
    .work-example
        width 250px
        max-width 250px
        height 357px
        transition .3s
        position relative
        border 5px solid var(--font-color)
        .example-image
            position absolute
            width 100%
            height 100%
            top 0
            background-size cover
            left 0
        &:hover
            transition .3s
            transform scale3d(1.05, 1.05, 1.05)
        .btn-container
            position absolute
            bottom 60px
            left -20px
            a 
                text-decoration none
                padding 1px 10px 
                border 3px solid
                font-size 20px
                font-weight 900
                background-color var(--background-color)
                &.github
                    color var(--red-color)
                    border-color var(--red-color)
                &.link
                    color var(--font-color)
                    border-color var(--font-color)
                    

</style>
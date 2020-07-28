<template>
    <div class="timeline" >
        <div class="years">
            <h5 v-for="(year,index) in years" :key="index" ref="years" class="year">{{year}}</h5>
        </div>
        <svg width="50" :height="lineLength + 20" ref="svg">
            <line x1="25" y1="10" x2="25" :y2="lineLength + 20" stroke-width="5" class="line" ref='line'/>
            <circle class="year-circle" v-for="index in years.length" :key="index" r="10" cx="25" :cy="--index * 150 + 10" ref="circle"/>
        </svg>
        <div class="experience-info">
            <div v-for="(exp, index) in experience" :key="index" class="experience-container" ref="expCont">
                <h5 class="year">{{years[index]}}</h5>
                <h3 class="job-title">{{exp.position}}</h3>
                <h4 class="company"><a :href="exp.website">{{exp.company}}</a></h4>
                <p class="description">{{exp.description}}</p>
            </div>
        </div>
        
    </div>
</template>

<script>
    import gsap from "gsap"
    import { ScrollTrigger } from "gsap/ScrollTrigger"

    gsap.registerPlugin(ScrollTrigger);
    export default {
        
        computed: {
            
            lineLength() {
                return this.experience.length  * 150
            },
            years(){
                return this.experience.map(r => {
                    const connect = r.endDate === "now"? 'till' : 'to';
                    return `${r.startDate} ${connect} ${r.endDate}` 
                })
            }
            
        },
        props: {
            experience: {
                type: Array 
            },
        },
        mounted () {
            const line = this.$refs.line;
            const circles = this.$refs.circle;
            const exp = this.$refs.expCont;
            const years = this.$refs.years;
            const tl = gsap.timeline({
                scrollTrigger: {
                    trigger: '.timeline'
                }
            })

            tl
              .to(line, {duration: 1, delay: 2, strokeDashoffset: 0})
              .to(circles, {opacity: 1, stagger: { each: .5 }})
              .to(exp, {x: 0, opacity: 1, stagger: { each: .5}}, '<')
              .to(years, {x: 0, opacity: 1, stagger: {each: .5}}, "<")
        },
    }
</script>

<style lang="stylus" scoped>
    .timeline
        display flex
        padding 0 50px
        @media screen and (max-width 800px)
            padding 0 0 25px 0
        .years
            display flex
            flex-direction column
            .year
                margin-bottom 133px
                transform translateX(-200px)
                opacity 0
            @media screen and (max-width 800px)
                display none
        .experience-info
            display flex
            flex-direction column
            max-width 700px
            margin-left 10px
            @media screen and (max-width 600px)
                flex-basis 70%
            .experience-container
                opacity 0
                transform translateX(200px)
                height 150px
                overflow-y auto
                text-overflow ellipsis
                @media screen and (max-width 400px)
                    height 130px
                    margin-bottom 20px
                .year
                    padding-bottom 10px
                    display none
                    @media screen and (max-width 800px)
                        display block
                .company
                    margin 10px 0 7px
                    a
                        text-decoration none 
                        color var(--red-color)
        .line
            stroke var(--background-third-color)
            stroke-dasharray 1000
            stroke-dashoffset 1000
        .year-circle
            fill var(--background-third-color)
            opacity 0
</style>
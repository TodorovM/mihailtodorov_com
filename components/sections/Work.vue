<template>
    <section id="work">
        <h1>Work Examples</h1>
        <div class="work-container">
            <WorkExample v-for="(ex, index) in workExamples" :key="index" :example="ex" />
        </div>
    </section>
</template>

<script>
    export default {
        data() {
            return {
                workExamples: [
                    {
                        image: 'website-cover.png',
                        github: 'https://github.com/TodorovM/mihailtodorov_com',
                        link: 'https://mihailtodorov.com'
                    },
                    {
                        image: 'lunch-cover.png',
                        github: 'https://github.com/TodorovM/random_lunch_finder',
                        link: 'https://focused-elion-5ba57a.netlify.app/'
                    },
                    {
                        image: 'vinyl-cover.png',
                        link: 'http://mihailtodorov.com/vinyl/'
                    },
                ]
            }
        },
    }
</script>

<style lang="stylus" scoped>
    #work
        padding 50px 100px
        .work-container
            padding 50px 0
            perspective 1000px
            display flex
            justify-content space-evenly

</style>
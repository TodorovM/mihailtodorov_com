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
                        image: 'work-cover.png',
                        github: 'https://github.com/TodorovM/mihailtodorov_com',
                        link: 'https://mihailtodorov.com'
                    }
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

</style>
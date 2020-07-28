<template>
    <section id="skills">
        <h1>Skills <span>&</span> Technologies</h1>
        <div class="skills-container">
            <DonutChart v-for="(skill, index) in skills" :key="index" :dashArray="skill.value" :text="skill.name" />
        </div> 
        <h1>Personal Skills <span>&</span> Other Technologies</h1>
        <div class="other-skills">
            <div class="personal">
                <h3>Personal</h3>
                <SkillChart v-for="(personalSkill, index) in personal" :key=index :text="personalSkill.name" :number="personalSkill.value" />
            </div>
            <div class="other">
                <h3>Other</h3>
                <SkillChart v-for="(otherSkill, index) in other" :key=index :text="otherSkill.name" :number="otherSkill.value" />
            </div>
        </div>
    </section>
</template>

<script>
    import skillConfig from './skills.config.js'
    export default {
        data() {
            return {
               skills: skillConfig.mainSkills,
               personal: skillConfig.personalSkills,
               other: skillConfig.otherSkills
            }
        },
    }
</script>

<style lang="stylus" scoped>
    #skills
        padding 50px 100px
        background-color var(--background-secondary-color)
        @media screen and (max-width: 620px)
            padding 50px 30px
        h1 
            margin 50px 0
        span 
            color var(--red-color)
        .skills-container
            display flex
            flex-wrap wrap
            justify-content center
        .other-skills
            display flex
            justify-content center
            @media screen and (max-width: 1024px)
                flex-direction column
                .other
                    border-left 0 !important
                    padding-left 0 !important
                    margin-top 50px
                >div
                    flex-basis 100%
            >div
                flex-basis 50%
                margin 0 10px
            .other
                border-left 1px solid var(--font-color)
                padding-left 10px
            
</style>
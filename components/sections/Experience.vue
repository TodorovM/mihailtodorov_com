<template>
    <section id="experience">
        <h1>My Work Experience</h1>
        <div class="experience-container">
            <Timeline :experience="experiences"/>
        </div>
    </section>
</template>

<script>
    export default {
        data() {
            return {
                experiences: [
                    {
                        position: 'Team Leader',
                        startDate: '05/2018',
                        endDate: 'now',
                        company: 'Dopamine',
                        website: 'https://www.dopamine.bg/',
                        description: 'I lead a team of junior FrontEnd Developers, Automation QA\'s and Game Animators. I plan work, projects and participate in the training of team members'
                    },
                    {
                        position: 'Customer Support / FrontEnd Developer',
                        startDate: '12/2017',
                        endDate: '04/2018',
                        company: 'SkyData ltd',
                        description: 'Working for a startup, my work included - supporting customers in a brand new hosting, creating WordPress themes and websites'
                    },
                    {
                        position: 'Training Manager / Assistant Manager',
                        startDate: '03/2017',
                        endDate: '11/2017',
                        company: 'WPX Hosting',
                        website: 'https://wpxhosting.com/',
                        description: 'Training new customer support agents. Doing quality assurance on chats and tickets.'
                    },
                    {
                        position: 'Customer Support',
                        startDate: '12/2016',
                        endDate: '03/2017',
                        company: 'WPX Hosting',
                        website: 'https://wpxhosting.com/',
                        description: 'Communicating with customers through tickets and chat. Managing their hosting accounts, domains, emails and payments'
                    },
                    {
                        position: 'Customer Support',
                        startDate: '09/2015',
                        endDate: '05/2016',
                        company: 'WPX Hosting',
                        website: 'https://wpxhosting.com/',
                        description: 'Communicating with customers through tickets and chat. Managing their hosting accounts, domains, emails and payments'
                    },
                ]
            }
        },
    }
</script>

<style lang="stylus" scoped>
    #experience
        h1
            padding 50px 100px
            @media screen and (max-width 440px)
                padding 50px 30px
        .experience-container
            max-width 1024px
            margin 50px auto
</style>
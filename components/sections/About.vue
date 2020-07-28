<template>
    <section id="about">
        <div class="about-container">
            <div class="about-picture">
                <div class="picture">
                    <img src="~assets/cut.png">
                    <div class="bordered"></div>
                </div>
            </div>
            <div class="about-text">
                <h2>Let me introduce myself</h2>
                <p>My name is <span>Mihail</span> and I have been working with computers since forever. </p>
                <p>I have 5 years working experience in the IT industry, where I have had a variety of positions
                ranging from <strong>Technical Support</strong> to <strong>Team Leader of a dev team</strong>.</p>
                <h2>More?</h2>
                <p>I was born and raised in Sofia and currently live here. I spend my free time usually reading, cooking (and eating), taking walks, playing with my cat or drawing and learning about new technologies.</p>
                <h2>What are my best qualities?</h2>
                <p>I am self-driven, independent and want to get the job done. I also love working with people</p>
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        
    }
</script>

<style lang="stylus" scoped>
    #about
        .about-container
            max-width 1024px
            margin 50px auto
            padding: 0 50px
            display flex
            align-items center
            @media screen and (max-width: 650px)
                flex-direction column
            span 
                color var(--red-color)
                font-weight 900
            h2 
                margin 40px 0 20px
                padding-bottom 5px
                border-bottom 1px solid var(--font-color)
            .about-picture
                margin-bottom 50px
                .picture
                    height 200px
                    width 200px
                    background-size cover
                    background-image url('~assets/profile.jpg')
                    border-radius 200px
                    position relative
                    margin-right 50px
                    img
                        position: absolute;
                        bottom: -46px;
                        width: 116px;
                        height: 151px;
                .bordered
                    height 246px
                    margin-left -2px
                    border-bottom 2px solid var(--font-color)
                    border-left 2px solid var(--font-color)
</style>
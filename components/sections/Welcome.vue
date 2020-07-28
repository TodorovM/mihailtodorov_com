<template>
  <section id="welcome">
      <div class="welcome-block">
        <div><h1 ref="firstText"></h1><span class="blinking-cursor" ref="blink1">▐</span></div>
        <div><h1 ref="secondText"></h1><span class="blinking-cursor" ref="blink2">▐</span></div>
        <div><h1 ref="thirdText"></h1><span class="blinking-cursor" ref="blink3">▐</span></div>
        <div><h1 ref="subtitle" class="subtitle"></h1><span class="blinking-cursor" ref="blink4">▐</span></div>
      </div>
    </section>
</template>

<script>
import gsap from "gsap";
import { TextPlugin } from "gsap/TextPlugin"

gsap.registerPlugin(TextPlugin);

export default {

data() {
    return {
        firstText: 'Hello!',
        secondText: 'My name is <span class="colored">Mihail Todorov</span>',
        subText: 'Welcome to my website!',
        options: ['websites', 'games', 'themes', 'fun things']
    }
},
computed: {
    thirdText() {
        return `and I make <span class="jumble">${[...Array(7)].map(r => r = String.fromCharCode(Math.floor(Math.random() * 94) + 32                                                                                     ))}</span>`
    }
},

methods: {
    async animate() {
        const tl = gsap.timeline();
        const { blink1, blink2, blink3, blink4, firstText, secondText, thirdText, subtitle } = this.$refs;

        await tl.set([blink2, blink3, blink4], {display: 'none'})
          .to(firstText, {duration: 0.5, delay: 2,  text: this.firstText})
          .set(blink1, {animation: 'none', opacity: 0})
          .set(blink2, {display: 'inline'})
          .to(secondText, {duration: 0.5, delay: 2,  text: this.secondText})
          .set(blink2, {animation: 'none', opacity: 0})
          .set(blink3, {display: 'inline'})
          .to(thirdText, {duration: 0.5, delay: 2,  text: this.thirdText})
          .add('jumble')
          .call(this.singleJumble, null, 'jumble')
          .set(blink3, {animation: 'none', opacity: 0, delay: 2})
          .set(blink4, {display: 'inline'})
          .to(subtitle, {duration: 0.5, delay: 2,  text: this.subText})
          .set(blink4, {animation: 'none', opacity: 0})
        
    }, 

    async jumble() {
        await this.singleJumble()
        setTimeout(() => this.jumble(), 2000)
        
    }, 

    async singleJumble() {
        const spanJumble = document.querySelector('.jumble');
        const otherOptions = this.options.filter(r => r !== spanJumble.innerText)
        const newText = otherOptions[Math.floor(Math.random() * (otherOptions.length))]

        for (let i = 1; i < 10; i++) {
           let scrambled = [...Array(Math.max(spanJumble.innerText.length, newText.length))]
                            .map(el => el = String.fromCharCode(Math.floor(Math.random() * 94) + 32)).join('')
            if (i % 9 === 0) scrambled = newText;
            await gsap.to(spanJumble, {duration: .1, text: scrambled}) 
        }
        
    }
},
mounted () {
    this.animate().then(_ => {this.jumble()});
},

}
</script>

<style lang='stylus'>
#welcome
    height 100vh
    width 100vw
    display flex
    justify-content center
    background-size cover
    background-color var(--background-color)
    background-image url('~assets/bg.jpg')
    background-blend-mode multiply
    .welcome-block
      max-width 400px
      width 400px
      padding 10px
      align-self center
      margin: 0 50px
      border-left 1px solid var(--font-color)
      div
        margin 2.5px 0
        &:last-child
            margin-top 30px
        .jumble 
            font-family 'Open Sans', sans-serif
            white-space nowrap
            @media screen and (max-width 500px)
                display block
                font-size 30px
        h1
            display inline
            height 35px
            font-size: 30px;
            font-weight 700
            .colored
                color var(--red-color)
                white-space nowrap
        .subtitle
            color var(--red-color)
            display inline
            font-weight 100
            font-size 20px
        .blinking-cursor
            color var(--red-color)
            font-size 25px
            animation blink 1s steps(2, end) infinite


@keyframes blink 
    from
        opacity 0
    
    to
        opacity 1

</style>
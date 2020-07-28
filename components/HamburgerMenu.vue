<template>
  <div>
    <div class="hamburger-menu" @click="animateHamburger">
      <div class="top bar"></div>
      <div class="middle bar"></div>
      <div class="bottom bar"></div>
    </div>
    <div class="menu-container">
        <a v-for="(link, index) in links" :key="index" :href="link" @click="scrollTo">
            {{ pages[index] }}
        </a>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
import {elastic} from "gsap/EasePack"
import {ScrollToPlugin} from "gsap/ScrollToPlugin"

gsap.registerPlugin(ScrollToPlugin);

export default {
  data() {
    return {
      clicked: false,
      pages: ['Welcome', 'About', 'Skills', 'Experience', 'Work', 'Contact']
    };
  },
  computed: {
      links() {
          return this.pages.map(r => `#${r.toLowerCase()}`) 
      }
  },
  methods: {
    async animateHamburger() {
      this.clicked = !this.clicked;
      const bars = document.querySelectorAll(".bar");
      const menu = document.querySelector('.menu-container');
      const menuLinks = document.querySelectorAll('.menu-container a')
      const tl = gsap.timeline();
      tl.timeScale(2)

      if (!this.clicked) {
        await tl
          .to([...menuLinks].reverse(), {y: '-=20', opacity: 0, stagger: {each: 0.3}})
          .to(bars[0], {duration: 1, rotate: "0deg", transformOrigin: "left",  ease: "elastic.out(1, 0.3)"})
          .to(bars[1], { duration: 1, rotate: "0deg",scale: 1, ease: "elastic.out(1, 0.3)"}, "<")
          .to(bars[2], { duration: 1, rotate: "0deg", transformOrigin: "right",  ease: "elastic.out(1, 0.3)" }, "<")
          .to(bars, {backgroundColor: '#ececec'}, '<')
          .to(menu, {duration: 0.5, width: 0, height: 0, borderRadius: '300px'}, "<")
      } else {
        await tl
          .to(bars[0], {duration: 1,rotate: "40deg",transformOrigin: "left center",  ease: "elastic.out(1, 0.3)"})
          .to(bars[1], { duration: 1, rotate: "-45deg", scaleX: 1.2, ease: "elastic.out(1, 0.3)" }, "<")
          .to(bars[2], { duration: 1, rotate: "40deg", transformOrigin: "right center",  ease: "elastic.out(1, 0.3)" }, "<")
          .to(bars, {backgroundColor: 'black'}, '<')
          .to(menu, {duration: 0.5, width: '100vw', height: '100vh', borderRadius: 0}, "<")
          .to([...menuLinks], {y: '+=20', opacity: 1, stagger: {each: 0.3}})
      }
    },
    scrollTo(e){
      this.clicked = true;
      this.animateHamburger().then(_ =>  gsap.to(window, {duration: 1, scrollTo: e.target.hash}));
    }
  }
};
</script>

<style lang="stylus" scoped>
.hamburger-menu 
  position fixed
  top 0
  right 0
  box-sizing content-box
  width 25px
  height 25px
  z-index 999
  margin 20px
  display flex
  flex-direction column
  justify-content space-between
  .bar 
    background-color var(--font-color)
    opacity 0.8
    height 2px
    border-radius 5px
  .top 
    width 50%
  .middle 
    width 100%
  .bottom 
    width 50%
    align-self flex-end
.menu-container
    background-color var(--font-color)
    border-radius 300px
    width 0
    height 0
    overflow-y scroll
    right 0
    z-index 99
    position fixed
    display flex
    flex-direction column
    justify-content center
    align-items center
    a 
        font-size: 30px
        text-decoration none 
        color black
        margin 10px 0 
        opacity 0
</style>
<template>
  <div id="app">
    <div v-if="!loaded" class="loader">
      <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
    </div>
    <Header></Header>
    <TopSection></TopSection>
    <About></About>
    <Advantages></Advantages>
    <Processors></Processors>
    <ProcessorsTable></ProcessorsTable>
    <Laptops></Laptops>
    <WhereToBuy></WhereToBuy>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from './components/header.vue'
import TopSection from './components/top-section.vue'
import About from './components/about.vue'
import Advantages from './components/advantages.vue'
import Processors from './components/processors.vue'
import ProcessorsTable from './components/processors-table.vue'
import Laptops from "@/components/laptops";
import WhereToBuy from "@/components/where-to-buy";
import Footer from "@/components/footer";

export default {
  name: 'App',
  components: {
    Header,
    TopSection,
    About,
    Advantages,
    Processors,
    ProcessorsTable,
    Laptops,
    WhereToBuy,
    Footer
  },
  data: () => {
    return {
      loaded: false
    }
  },
  mounted() {
    setTimeout(() => {
      this.loaded = true;
    }, 500);
  }
}
</script>

<style lang="stylus">

@font-face
  font-family 'Uni'
  src url('~@/assets/fonts/UniSansHeavyItalic.eot')
  src url('~@/assets/fonts/UniSansHeavyItalic.eot?#iefix') format('embedded-opentype'), url('~@/assets/fonts/UniSansHeavyItalic.woff') format('woff'), url('~@/assets/fonts/UniSansHeavyItalic.ttf') format('truetype')
  font-weight 900
  font-style normal
  font-display swap

@font-face
  font-family 'Noto'
  src url('~@/assets/fonts/notosans.eot')
  src url('~@/assets/fonts/notosans.eot?#iefix') format('embedded-opentype'), url('~@/assets/fonts/notosans.woff') format('woff'), url('~@/assets/fonts/notosans.ttf') format('truetype')
  font-weight normal
  font-style normal
  font-display swap

@font-face
  font-family 'Noto'
  src url('~@/assets/fonts/notosansbold.eot')
  src url('~@/assets/fonts/notosansbold.eot?#iefix') format('~@/assets/embedded-opentype'), url('~@/assets/fonts/notosansbold.woff') format('woff'), url('~@/assets/fonts/notosansbold.ttf') format('truetype')
  font-weight bold
  font-style normal
  font-display swap

*
  box-sizing border-box
:root
  --accent #FF7D00
  --gradient linear-gradient(90deg, #E4700D 0%, #9E151C 100%)
  --gradient2 linear-gradient(210.56deg, #312E3A 14.97%, #291A41 44.38%)
  --gray #F4F4F4
  --gray2 #F0F0F3
  --gray3 #5A5B5B
body
  margin 0
  font-family 'Noto', sans-serif
  font-size 16px
#app
  max-width 100%
  overflow hidden
section
  position relative
.container
  max-width 1280px
  margin auto
  @media (max-width 1279px)
    padding 0 20px

.heading
  font-family 'Uni', sans-serif
  font-size 60px
  text-transform uppercase
  line-height 1.2
  letter-spacing 0.03em
  @media (max-width 1279px)
    font-size 50px
  @media (max-width 1023px)
    font-size 32px
  &--white
    color #fff
  &__accent
    color var(--accent)
  &__small
    font-size .66em

a
button
  cursor pointer
  border none
  text-decoration none
  background transparent

.btn-group
  display flex
  flex-wrap wrap
  .btn
    margin-right 30px
    @media (max-width 1279px)
      margin-right 10px
.btn
  display inline-block
  font-family 'Uni', sans-serif
  font-size 18px
  text-transform uppercase
  padding 1.1em 1.6em 1em
  border 3px solid #000
  text-decoration none
  color #000
  letter-spacing .03em
  overflow hidden
  position relative
  z-index 2
  @media (max-width 1279px)
    padding 1.1em 1em 1em
  @media (max-width 1023px)
    font-size 12px
  &::before
    content ''
    display block
    width 1em
    height 1em
    position absolute
    top -.5em
    right -.5em
    transform rotate(45deg)
    background #000
    transition transform .5s, color .5s
    z-index -1
  &--accent
    border-color var(--accent)
    color var(--accent)
    &::before
      background var(--accent)
  &:hover
    @media (hover)
      color #fff
      &::before
        transform scale(50) rotate(45deg)
  &--buy
    background var(--accent)
    color #fff
    border none
    font-size 14px
    padding 12px 12px 9px
    transition background-color .5s ease-in-out
    &::before
      display none
    &:hover
      @media (hover)
        background-color #000

.loader
  position fixed
  top 0
  left 0
  width 100vw
  height 100vh
  background #fff
  display flex
  align-items center
  justify-content center
  z-index: 99
  .lds-ring
    display inline-block
    position relative
    width 80px
    height 80px
    div
      box-sizing border-box
      display block
      position absolute
      width 64px
      height 64px
      margin 8px
      border 8px solid #fff
      border-radius 50%
      animation lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite
      border-color var(--accent) transparent transparent transparent
      &:nth-child(1)
        animation-delay -0.45s
      &:nth-child(2)
        animation-delay -0.3s
      :nth-child(3)
        animation-delay -0.15s

@keyframes lds-ring
  0%
    transform rotate(0deg)
  100%
    transform rotate(360deg)
</style>

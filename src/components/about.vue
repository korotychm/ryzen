<template>

  <section class="about" id="about">
    <div class="container">
      <h2 class="heading"><span class="heading__small">Взгляни на свой ноутбук </span><span class="heading__accent">по-новому</span></h2>
      <div class="carousel" id="carousel">
        <div class="carousel__nav">
          <button class="carousel__arrow carousel__arrow--prev"
                  @click="prevSlide"
                  :class="{ 'carousel__arrow--disabled': !canPrev }"
          ></button>
          <button class="carousel__arrow carousel__arrow--next"
                  @click="nextSlide"
                  :class="{ 'carousel__arrow--disabled': !canNext }"
          ></button>
        </div>
        <div class="carousel__wrapper">
          <div class="carousel__track" :style="trackStyles">
            <div class="carousel__slide"
                 v-for="(slide, index) in slides"
                 :key="index"
                 :style="slideStyles"
            >
              <div class="carousel__card">
                <div class="carousel__img">
                  <img width="277" height="212" :src="slide.img" alt=""/>
                </div>
                <h3>{{ slide.title }}</h3>
                <p>{{ slide.text }}</p><a class="btn btn--accent" :href="slide.ref">{{ slide.btnText }}</a>
              </div>
            </div>
          </div>
        </div>
      </div>
      <h2 class="heading heading--white">
        <span class="heading__small">Мобильные процессоры</span>
        <span class="heading__small heading__accent">AMD Ryzen™ 4000 серии с графикой Radeon™</span>
      </h2>
      <div class="about__logos">
        <img width="397" height="254px" src="../assets/img/about/ryzen-logo.svg" />
        <img width="485" height="154px" src="../assets/img/about/radeon-logo.svg" />
      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: 'About',
  data: () => {
    return {
      showNav: false,
      slides: [
        {
          title: 'Ты разрядишься раньше, чем твой ноутбук',
          text: 'Энергоэффективность процессоров Ryzen 4000 до двух раз выше по сравнению с процессорами предыдущего поколения.',
          img: require('../assets/img/about/slide1.svg'),
          btnText: 'Ноутбуки с долгим зарядом',
          ref: 'filter1'
        },
        {
          title: 'Ноутбук легко заменит стационарный ПК',
          text: 'Мощность процессоров Ryzen позволяет работать даже в самых требовательных приложениях, подключая несколько мониторов с разрешением 4К.',
          img: require('../assets/img/about/slide2.svg'),
          btnText: 'Мощные ноутбуки для работы',
          ref: 'filter2'
        },
        {
          title: 'Ультралегкий ноутбук может быть мощным',
          text: 'Максимально возможное количество ядер для ультратонкого компьютера предоставляет потрясающую произодительность.',
          img: require('../assets/img/about/slide1.svg'),
          btnText: 'Ультралегкие ноутбуки',
          ref: 'filter3'
        },
        {
          title: 'Ноутбук может быть игровым',
          text: 'Максимально возможное количество ядер для ультратонкого компьютера предоставляет потрясающую произодительность.',
          img: require('../assets/img/about/slide2.svg'),
          btnText: 'Ультралегкие ноутбуки',
          ref: 'filter3'
        },
        {
          title: 'Ты разрядишься раньше, чем твой ноутбук',
          text: 'Энергоэффективность процессоров Ryzen 4000 до двух раз выше по сравнению с процессорами предыдущего поколения.',
          img: require('../assets/img/about/slide1.svg'),
          btnText: 'Ноутбуки с долгим зарядом',
          ref: 'filter1'
        },
        {
          title: 'Ноутбук легко заменит стационарный ПК',
          text: 'Мощность процессоров Ryzen позволяет работать даже в самых требовательных приложениях, подключая несколько мониторов с разрешением 4К.',
          img: require('../assets/img/about/slide2.svg'),
          btnText: 'Мощные ноутбуки для работы',
          ref: 'filter2'
        },
        {
          title: 'Ультралегкий ноутбук может быть мощным',
          text: 'Максимально возможное количество ядер для ультратонкого компьютера предоставляет потрясающую произодительность.',
          img: require('../assets/img/about/slide1.svg'),
          btnText: 'Ультралегкие ноутбуки',
          ref: 'filter3'
        },
        {
          title: 'Ноутбук может быть игровым',
          text: 'Максимально возможное количество ядер для ультратонкого компьютера предоставляет потрясающую произодительность.',
          img: require('../assets/img/about/slide2.svg'),
          btnText: 'Ультралегкие ноутбуки',
          ref: 'filter3'
        }
      ],
      currentSlide: 0,
      slidesToShow: {
        '300' : 1,
        '767' : 2,
        '1023' : 3
      },
      windowWidth: 0,
      slideWidth: 0,
      slidesShown: 0,
      canPrev: false,
      canNext: true,
    }
  },
  computed: {
    slideStyles: function () {
      return {
        width: this.slideWidth + 'px'
      }
    },
    trackStyles: function () {
      let shift = this.slideWidth * this.currentSlide;
      return {
        transform: 'translateX(-' + shift + 'px)'
      }
    }
  },
  methods: {

    getSlideWidth() {
      this.windowWidth = window.innerWidth;
      for (let viewport in this.slidesToShow) {
        if (this.windowWidth > viewport) this.slidesShown = this.slidesToShow[viewport];
      }
      this.slideWidth = document.getElementsByClassName("carousel__wrapper")[0].offsetWidth / this.slidesShown;
    },

    checkCarouselNav() {
      this.canPrev = (this.currentSlide !== 0);
      this.canNext = (this.currentSlide < (this.slides.length - this.slidesShown));
    },

    prevSlide() {
      if (this.canPrev) this.currentSlide--;
      this.checkCarouselNav();
    },
    nextSlide() {
      if (this.canNext) this.currentSlide++;
      this.checkCarouselNav();
    },

  },
  mounted: function () {
    this.getSlideWidth();
    window.addEventListener("resize", this.getSlideWidth);
  }
}
</script>

<style lang="stylus">
.about
  margin-top 150px
  padding 30px 0 0
  position relative
  @media (max-width 1279px)
    margin-top 70px
  @media (max-width 767px)
    margin-top 150px
  &::before
    content ''
    display block
    width 1920px
    height 1100px
    position absolute
    top 350px
    left 50%
    transform translateX(-50%)
    z-index -1
    background url(../assets/img/about/bg.svg) no-repeat center
    @media (max-width 1279px)
      width 1800px
      height 900px
      background-size contain
      top auto
      bottom -100px
    @media (max-width 1023px)
      width 1200px
      height 600px
      bottom -130px
  .heading
    margin 0 0 60px
    @media (max-width 1279px)
      margin-bottom 30px
    span
      display block
  &__logos
    display flex
    align-items flex-start
    margin-top 120px
    img:last-child
      margin-left 180px
      margin-top: 5px
    @media (max-width 1279px)
      margin-top 50px
      justify-content space-between
      img
        width 38%
        height auto
        &:last-child
          margin-left 0
          margin-top 2px
          width 46%

.carousel
  padding-right 120px
  position relative
  margin-bottom 100px
  @media (max-width 1279px)
    padding-right 0
    margin-bottom 70px
  &__nav
    display flex
    justify-content space-between
    width 140px
    position absolute
    top -130px
    right 100px
    @media (max-width 1023px)
      flex-direction column
      justify-content flex-end
      padding-bottom 23px
      background var(--gray)
      height 100%
      width 30px
      right -20px
      top 0
      z-index 3
  &__arrow
    width 60px
    height 60px
    border 3px solid var(--accent)
    border-radius 50%
    background transparent
    padding-left 10px
    transition opacity .5s, border-color .5s
    touch-action manipulation
    @media (max-width 1023px)
      width 50px
      height 50px
      margin 10px 0 10px -30px
      background #fff
    &::after
      content ''
      width 20px
      height 20px
      display block
      border-right 3px solid var(--accent)
      border-bottom 3px solid var(--accent)
      transform: rotate(-45deg)
      transition border-color .5s
      @media (max-width 1023px)
        width 15px
        height 15px
    &--prev
      transform: rotate(180deg)
    &--disabled
      border-color var(--gray3)
      pointer-events none
      &::after
        border-color var(--gray3)
    &:hover
      @media (hover)
        opacity .8
  &__wrapper
    max-width 100%
  &__track
    display inline-flex
    margin 0 -20px
    transition transform .5s ease-in-out
  &__slide
    padding 0 20px
    flex-shrink 0
    @media (max-width 1279px)
      padding 0 10px
  &__card
    background var(--gray)
    padding 40px 35px
    @media (max-width 767px)
      padding 30px 20px
    img
      width 100%
      height auto
      display block
    h3
      font-size 20px
      font-family 'Uni', sans-serif
      text-transform uppercase
      margin 2em 0 1em
      line-height 1.3
      @media (max-width 1279px)
        font-size 18px
    p
      font-size 14px
      line-height 1.4
      margin 0
      min-height 95px
      @media (max-width 1279px)
        font-size 12px
        min-height 70px
    .btn
      font-size 12px
      margin-top 30px
</style>

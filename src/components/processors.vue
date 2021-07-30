<template>

  <section id="compare" class="processors">
    <div class="container">
      <h1 class="heading heading--white">
        <span class="heading__small">Выбери свой</span>
        <span class="heading__accent">AMD RYZEN</span>
      </h1>
      <div class="processors__cards">

        <div v-for="(item,index) in items" :key="index" class="processors__card">
          <div class="processors__title">
            <img width="120" height="106" :src="item.img" :alt="'Лого ' + item.title"/>
            <h3>{{ item.title }}</h3>
          </div>
          <p>{{ item.text }}</p>
          <h4>Идеально подходит для</h4>
          <div class="processors__icons">
            <div v-for="(icon,index) in item.icons" :key="index" class="processors__icon">
              <img width="60" height="45" :src="icon.icon" alt=""/>
              <p>{{ icon.text }}</p>
            </div>
          </div>
          <div class="processors__btn">
            <a @click="simulateClick(item.selector)" href="#laptops" class="btn btn--accent">{{ item.btn }}</a>
          </div>
        </div>

      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: 'Processors',
  data: () => {
    return {
      items: [
        {
          title: 'AMD RYZEN™ 7 4000 серии',
          img: require('../assets/img/processors/ryzen7.png'),
          text: 'Ускорьте выполнение любых задач, включая работу в ресурсоемких приложениях, требующих высокой производительности.',
          btn: 'Ноутбуки на Ryzen 7',
          selector: '[value="Ryzen 7"]',
          icons: [
            {
              icon: require('../assets/img/processors/icon1.svg'),
              text: 'Быстрого редактирования видео- и фотоматериалов'
            },
            {
              icon: require('../assets/img/processors/icon2.svg'),
              text: 'Одновременного выполнения нескольких ресурсоемких задач'
            },
            {
              icon: require('../assets/img/processors/icon3.svg'),
              text: 'Любимых игр в разрешении Full HD'
            },
            {
              icon: require('../assets/img/processors/icon4.svg'),
              text: 'Путешествий (длительная автономность)'
            }
          ]
        },
        {
          title: 'AMD RYZEN™ 5 4000 серии',
          img: require('../assets/img/processors/ryzen5.png'),
          text: 'Безупречная производительность для работы с мультимедийным контентом и развлечений.',
          btn: 'Ноутбуки на Ryzen 5',
          selector: '[value="Ryzen 5"]',
          icons: [
            {
              icon: require('../assets/img/processors/icon5.svg'),
              text: 'Простого редактирования фото и видео'
            },
            {
              icon: require('../assets/img/processors/icon6.svg'),
              text: 'Эффективной многозадачности'
            },
            {
              icon: require('../assets/img/processors/icon7.svg'),
              text: 'Потоковой трансляции фильмов в разрешении 4K'
            },
            {
              icon: require('../assets/img/processors/icon4.svg'),
              text: 'Командировок (высокая автономность)'
            }
          ]
        },
        {
          title: 'AMD RYZEN™ 3 4000 серии',
          img: require('../assets/img/processors/ryzen3.png'),
          text: 'Базовый вариант при выборе высокопроизводительного ноутбука. Работайте в Интернете, ведите потоковую трансляцию, творите с уверенностью.',
          btn: 'Ноутбуки на Ryzen 3',
          selector: '[value="Ryzen 3"]',
          icons: [
            {
              icon: require('../assets/img/processors/icon8.svg'),
              text: 'Потоковой трансляции видео с разрешением 4K'
            },
            {
              icon: require('../assets/img/processors/icon9.svg'),
              text: 'Быстрой загрузки веб-сайтов и одновременной работы с несколькими документами'
            },
            {
              icon: require('../assets/img/processors/icon10.svg'),
              text: 'Общения с друзьями в социальных сетях'
            },
            {
              icon: require('../assets/img/processors/icon4.svg'),
              text: 'Достаточное время работы от батареи'
            }
          ]
        }
      ]
    }
  },
  methods: {
    simulateClick(selector) {
      document.querySelector(selector).click();
    }
  }
}
</script>

<style lang="stylus">
.processors
  padding-top 100px
  position relative
  @media (max-width 1279px)
    padding-top 50px
  &::before
    content ''
    display block
    width 1920px
    height 690px
    position absolute
    top -50px
    left 50%
    transform translateX(-50%)
    z-index -1
    background url(../assets/img/processors/bg.svg) no-repeat center
  .heading
    margin 0
    padding-left 730px
    @media (max-width 1279px)
      padding-right 50px
      padding-left 550px
    @media (max-width 1023px)
      padding-left 0
      text-align right
    span
      display block
  &__cards
    margin-top 60px
    display grid
    grid-template-columns minmax(0,1fr) minmax(0,1fr) minmax(0,1fr)
    grid-gap 40px
    @media (max-width 1279px)
      grid-gap 30px
    @media (max-width 767px)
      margin-top 30px
      grid-template-columns 1fr
  &__card
    padding 35px
    background var(--gray)
    @media (max-width 1279px)
      padding 20px
    > p
      font-size 14px
      margin 0 0 30px
      min-height 80px
      @media (max-width 1023px)
        font-size 12px
        min-height 110px
      @media (max-width 767px)
        min-height 0
    h4
      font-size 14px
      font-weight bold
      margin 0 0 35px
  &__btn
    text-align center
    margin-bottom 10px
    .btn
      font-size 12px
  &__title
    display flex
    align-items center
    margin-bottom 25px
    @media (max-width 768px) and (min-width 500px)
      display block
      margin-bottom 10px
    img
      flex-shrink 0
      margin-right 25px
      width 120px
      height auto
      @media (max-width 768px) and (min-width 500px)
        margin 0
        width 100%
    h3
      font-size 26px
      font-family 'Uni', sans-serif
      text-transform uppercase
      @media (max-width 1279px)
        font-size 18px
      @media (max-width 1023px)
        font-size 22px
        margin-bottom 0
      @media (max-width 767px)
        font-size 18px
  &__icons
    display grid
    grid-template-columns 1fr 1fr
    grid-gap 40px
    margin-bottom 65px
    @media (min-width 500px) and (max-width 768px)
      grid-template-columns 1fr
    @media (max-width 1279px)
      grid-gap 20px
      margin-bottom 30px
    p
      margin 10px 0 0
      font-size 11px
      color var(--gray3)
      @media (max-width 1023px)
        margin-bottom 20px
</style>

<template>

  <section class="top-section">
    <div class="container">
      <div class="top-section__text">
        <h1 class="heading">Целая вселенная<br /><span class="heading__accent">в твоём ноутбуке</span></h1>
        <p>Редактируйте видео, смотрите потоковые трансляции в формате Ultra HD 4K
          и наслаждайтесь плавностью игрового процесса в самых популярных видеоиграх.
          Получите ноутбук с мощностью настольного ПК благодаря мобильному
          процессору AMD Ryzen™ 4000 серии с графикой Radeon™, который обеспечивает
          потрясающее время автономной работы в элегантном форм-факторе.</p>
        <div class="btn-group">
          <a class="btn" href="#about">Узнай больше</a>
          <a class="btn btn--accent" href="#laptops">Выбери ноутбук</a>
        </div>
      </div>
      <div class="top-section__img">
        <img width="915" height="1192" src="../assets/img/top-section/top-section.svg" />
      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: 'TopSection'
}
</script>

<style lang="stylus">
.top-section
  padding-top 50px
  @media (max-width 767px)
    padding-top 20px
    padding-bottom 50px
  .container
    position relative
    &::after
      content ''
      display block
      width 1000px
      height 1000px
      position absolute
      right 0
      top -330px
      background url(../assets/img/top-section/ryzen-logo-bg.svg) no-repeat center
      background-size contain
      pointer-events none
      z-index -1
      @media (max-width 767px)
        width 300px
        height 300px
        top auto
        bottom -170px
        right 100px
  &__text
    width 50%
    position relative
    @media (max-width 767px)
      width 100%
    .heading
      margin 0 0 30px
      @media (max-width 1279px)
        margin-bottom 15px
    p
      font-size 18px
      line-height 1.5
      margin 0 0 15px
      @media (max-width 1023px)
        font-size 14px
        line-height 1.3
    .btn-group
      margin-top 80px
      @media (max-width 767px)
        display block
        width 50%
        margin-top 40px
        .btn
          margin-bottom 10px
  &__img
    position absolute
    top -350px
    right -290px
    @media (min-width: 1600px)
      right -330px
    @media (max-width 1279px)
      width 500px
      right -30px
      top -190px
      img
        width 100%
        height auto
    @media (max-width 1023px)
      top auto
      bottom -130px
      width 500px
      right -130px
    @media (max-width 767px)
      width 375px
      right -155px
      bottom -290px
</style>

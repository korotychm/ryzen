<template>

  <section class="where-to-buy" id="buy">
    <div class="container">
      <h2 class="heading heading--white">Где купить?</h2>
      <div class="where-to-buy__partner">
        <div class="where-to-buy__logo">
          <img width="452" height="96" src="../assets/img/where-to-buy/citilink.svg" alt="Логотип Ситилинк"/>
        </div>
        <div class="where-to-buy__text">
          <p>«Ситилинк» – одна из крупнейших сетей магазинов электроники и бытовой техники, входит в ГК Merlion. На рынке с 2008 года.</p>
          <p>В инфраструктуре компании интернет-магазин citilink.ru, более 650 магазинов и пунктов выдачи заказов в 360 городах России.</p>
          <a class="btn btn--accent" href="https://citilink.ru" target="_blank">В магазин!</a>
        </div>
      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: 'WhereToBuy'
}
</script>

<style lang="stylus">
.where-to-buy
  padding 100px 0 0
  position relative
  min-height 740px
  @media (max-width 767px)
    padding-top 50px
    min-height 0
  &::before
    content ''
    display block
    width 1920px
    height: 1100px
    position absolute
    top -290px
    left 50%
    transform translateX(-50%)
    z-index -1
    background url(../assets/img/where-to-buy/bg.svg) no-repeat center
    @media (max-width 767px)
      top -400px
  &__partner
    display grid
    grid-template-columns 2fr 3fr
    margin-top 90px
    grid-gap 150px
    @media (max-width 1279px)
      grid-gap 50px
    @media (max-width 767px)
      grid-template-columns 1fr
      grid-gap 30px
      margin-top 60px
  &__text
    color #fff
    font-size 18px
    @media (max-width 1279px)
      font-size 16px
    @media (max-width 767px)
      font-size 14px
    .btn
      margin-top 30px
      @media (max-width 767px)
        width 100%
        text-align center
  &__logo
    @media (max-width 1279px)
      margin-top 50px
    @media (max-width 767px)
      margin-top 0
    img
      width 100%
      height auto

</style>

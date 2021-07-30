<template>

  <footer class="footer" id="subscribe">
    <div class="container">
      <h2 class="heading">
        Узнай больше
        <span class="heading__accent">о продуктах AMD</span>
      </h2>
      <div class="subscribe">
        <div class="subscribe__text">
          Оставь свой E-mail и получай новости и технические обзоры новых продуктов AMD. Будь в числе первых покупателей новинок!
        </div>
        <div class="subscribe__form">
          <form @submit.prevent="processForm">
            <input type="text" v-model="email" placeholder="Ваш E-mail"/>
            <button class="btn btn--accent">Подписаться</button>
          </form>
          <p class="subscribe__agree">
            Нажимая кнопку “Подписаться” я даю свое согласие на обработку персональных данных на условиях, определенных <a>Политикой конфиденциальности</a>
          </p>
        </div>
      </div>
      <a class="to-top" href="#top">
        к началу
      </a>
    </div>
  </footer>

</template>

<script>
export default {
  name: 'Footer',
  data: () => {
    return {
      email: '',
      ajaxRequest: ''
    }
  },
  methods: {
    processForm() {
      console.log(this.email);
    }
  }
}
</script>

<style lang="stylus">
.footer
  .container
    padding 50px 0 200px
    position relative
    @media (max-width 1279px)
      padding 50px 20px 120px
    @media (max-width 767px)
      padding 150px 20px 120px
      .heading span
        display block
  .to-top
    width 120px
    height 120px
    position absolute
    bottom 0
    left 0
    background var(--accent)
    background-image url('../assets/img/footer/arrow.svg')
    background-repeat no-repeat
    background-position center 20px
    color #fff
    cursor pointer
    transition opacity .5s
    text-align center
    padding-top 80px
    font-weight bold
    @media (max-width 1023px)
      width 60px
      height 60px
      font-size 0
      background-size contain
      background-position center
      padding 0
    &:hover
      @media (hover)
        opacity .8
.subscribe
  display grid
  grid-template-columns 1fr 2fr
  grid-gap 80px
  @media (max-width 1023px)
    grid-template-columns 1fr
    grid-gap 30px
  &__text
    font-size 18px
    @media (max-width 1279px)
      font-size 14px
  &__agree
    color var(--gray3)
    font-size 12px
    margin-top 20px
    @media (max-width 1023px)
      font-size 10px
    a
      cursor pointer
      color var(--accent)
  &__form
    display flex
    flex-wrap wrap
    max-width 550px
    form
      width 100%
    input
      width 350px
      border 3px solid var(--accent)
      font-family 'Uni', sans-serif
      font-size 18px
      text-transform uppercase
      padding 1.1em 1.6em 1em
      outline none !important
      -webkit-appearance none
      border-radius 0
      @media (max-width 1023px)
        width calc(100% - 119px)
        font-size 12px
      &::placeholder
        color #ccc
    .btn
      margin-left -3px
</style>

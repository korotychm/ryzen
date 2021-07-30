<template>

  <header class="header" id="top">

    <div class="container">
      <a class="header__logo" href="/">
        <img width="200" height="76" src="../assets/img/logo.svg" alt="Логотип AMD Ryzen"/>
      </a>
    </div>

    <button class="burger" @click="showNav = !showNav" :class="{ 'active': showNav }">
      <div></div>
      <div></div>
      <div></div>
    </button>

    <nav class="nav">
      <a
          v-for="item in navItems"
          :key="item.name"
          :href="item.href"
          class="nav__item"
      >
        {{ item.name }}
      </a>
    </nav>

  </header>

</template>

<script>

export default {
  name: 'Header',
  data: () => {
    return {
      showNav: false,
      navItems: [
        {
          name: 'О процессорах Ryzen',
          href: '#about'
        },
        {
          name: 'Преимущества',
          href: '#advantages'
        },
        {
          name: 'Сравнение процессоров',
          href: '#compare'
        },
        {
          name: 'Технические характеристики',
          href: '#tech'
        },
        {
          name: 'Ноутбуки на базе Ryzen',
          href: '#laptops'
        },
        {
          name: 'Где купить?',
          href: '#buy'
        },
        {
          name: 'Узнай больше',
          href: '#subscribe'
        }
      ]
    }
  }
}

</script>

<style lang="stylus">

.header
  padding 30px 0
.nav
  position fixed
  right 0
  top 0
  height 100vh
  background var(--gradient2)
  padding 150px 80px
  z-index 9
  transform translateX(100%)
  transition transform .7s ease-in-out
  opacity .9
  @media (max-width 767px)
    padding 120px 50px
    width 100vw
  a
    display block
    color #fff
    text-transform uppercase
    font-size 24px
    font-family 'Uni', sans-serif
    margin-bottom 1em
    transition color .5s
    @media (max-width 767px)
      font-size 21px
    &:hover
      @media (hover)
        color var(--accent)
.burger
  position fixed
  top 0
  right 0
  width 80px
  height 80px
  background var(--accent)
  padding 18px 25px
  transition opacity .5s
  z-index 10
  @media (max-width 767px)
    width 60px
    height 60px
    padding 8px 15px
  &:hover
    @media (hover)
      opacity .9
  div
    width 100%
    height 3px
    background #fff
    margin 8px 0
    transition transform .7s, opacity .3s
  &.active
    div:nth-child(1)
      transform translateY(11px) rotate(45deg)
    div:nth-child(2)
      opacity 0
    div:nth-child(3)
      transform translateY(-11px) rotate(-45deg)
    ~ .nav
      transform translateX(0)

</style>

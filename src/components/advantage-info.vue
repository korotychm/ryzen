<template>

  <div class="advantages__info">
    <div class="advantages__heading">
      <img width="80" height="80" :src="icon" />
      <h3>{{ title }}</h3>
    </div>
    <p>{{ text }}</p>
  </div>

</template>

<script>

export default {
  name: 'AdvantageInfo',
  props: ['title','text','icon'],
}

</script>

<style lang="stylus">

.advantages__heading
  display flex
  align-items center
  margin-bottom 20px
  img
    flex-shrink 0
    margin-right 25px
    @media (max-width 1279px)
      width 60px
      height auto
      margin-right 20px
  h3
    font-family 'Uni', sans-serif
    font-size 20px
    text-transform uppercase
    padding-right 10px
    margin 0
    @media (max-width 1279px)
      font-size 18px
.advantages__info
    @media (max-width 1279px)
      font-size 14px

</style>


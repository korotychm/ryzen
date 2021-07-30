<template>

  <section id="advantages">
    <div class="container">
      <div class="advantages">

        <div v-for="(item,index) in items" :key="index" class="advantages__item">
          <AdvantageInfo
              :title="item.title"
              :text="item.text"
              :icon="item.icon"
          ></AdvantageInfo>
          <AdvantageGraph
              :title="item.graphTitle"
              :counter="item.counter"
              :counterCaption="item.counterCaption"
              :isTarget="item.isTarget"
          ></AdvantageGraph>
        </div>

      </div>
      <div class="btn-group">
        <a class="btn" href="#compare">Сравни процессоры</a>
        <a class="btn btn--accent" href="#laptops">Выбери ноутбук</a>
      </div>
    </div>
  </section>

</template>

<script>
import AdvantageInfo from '@/components/advantage-info.vue'
import AdvantageGraph from "@/components/advantage-graph";

export default {
  name: 'Advantages',
  components: {
    AdvantageGraph,
    AdvantageInfo
  },
  data: () => {
    return {
      items: [
        {
          title: 'Превосходная производительность',
          text: 'Создание контента, потоковая трансляция и работа в многозадачном режиме быстрее, чем когда-либо. И все это благодаря самому высокопроизводительному процессору для ультратонких ноутбуков.',
          icon: require('../assets/img/advantages/advantage1.svg'),
          graphTitle: '* Cinebench 15 64-bit multi-core',
          counter: [672,1568],
          counterCaption: ['Ryzen 7 3700U','Ryzen 7 4800U'],
          isTarget: [false,true]
        },
        {
          title: 'Потрясающая графика',
          text: 'Лучшая в своём классе видеокарта для ультратонких ноутбуков предлагает невероятные возможности. Наслаждайтесь потоковой трансляцией с разрешением 4К и играми в Full HD.',
          icon: require('../assets/img/advantages/advantage2.svg'),
          graphTitle: '* 3DMark Fire Strike Graphics',
          counter: [2272,3899],
          counterCaption: ['графика Radeon в Ryzen 7 3700U','графика Radeon в Ryzen 7 4800U'],
          isTarget: [false,true]
        },
        {
          title: 'Максимальная мобильность',
          text: 'Энергоэффективность процессоров Ryzen 4000 серии до двух раз выше по сравнению с процессорами предыдущего поколения, что гарантирует длительное время работы от батареи вашего ноутбука.',
          icon: require('../assets/img/advantages/advantage3.svg'),
          graphTitle: '* Часов работы в режиме браузера',
          counter: [7,12],
          counterCaption: ['HP Envy X360 13, Ryzen 7 3700U','HP Envy X360 13, Ryzen 7 4700U'],
          isTarget: [false,true]
        }
      ]
    }
  }
}
</script>

<style lang="stylus">
.advantages
  margin 150px 0 110px
  display grid
  grid-template-columns minmax(0,1fr) minmax(0,1fr) minmax(0,1fr)
  grid-gap 100px
  @media (max-width 1279px)
    grid-gap 70px
    margin-bottom 100px
    & + .btn-group
      margin-bottom 50px
  @media (max-width 1023px)
    margin-bottom 50px
    grid-template-columns 1fr
    grid-gap 50px

</style>

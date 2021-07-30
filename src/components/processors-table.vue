<template>

  <section class="processors-table" id="tech">
    <div class="container">
      <div class="table">
        <div class="tr tr--th">
          <div v-for="(th,index) in thead" :key="index" class="td">
            {{ th }}
          </div>
        </div>
        <div v-for="(item,index) in items" :key="index" class="tr">
          <div class="td td--title">
            <img width="100" height="89" :src="item.img" :alt="'Лого' + item.name" />
            <div>
              <span>{{ item.name }}</span>
              <span>{{ item.model }}</span>
            </div>
          </div>
          <div v-for="(td,key) in itemsSliced[index]" :key="key" class="td">
            {{ td }}
          </div>
        </div>
      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: 'ProcessorsTable',
  data: () => {
    return {
      thead: [
          'AMD Ryzen 4000 серии',
          'Ядер/потоков',
          'Архитектура',
          'TDP',
          'Макс.частота',
          'Ядер ГП',
          'Частота ГП',
          'Кэш-память',
          'Возможности подключения',
          'Совместимость дисплея'
      ],
      items: [
        {
          name: 'Ryzen 7',
          model: '4800H',
          img: require('../assets/img/processors/ryzen7.png'),
          cores: '8/16',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '45 Вт',
          frequency: '4.2 ГГц',
          graphicCores: '7',
          graphicFrequency: '1600 МГц',
          cash: '12 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        },
        {
          name: 'Ryzen 7',
          model: '4600H',
          img: require('../assets/img/processors/ryzen7.png'),
          cores: '6/12',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '45 Вт',
          frequency: '4.0 ГГц',
          graphicCores: '6',
          graphicFrequency: '1500 МГц',
          cash: '11 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        },
        {
          name: 'Ryzen 7',
          model: '4800U',
          img: require('../assets/img/processors/ryzen7.png'),
          cores: '8/16',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '15 Вт',
          frequency: '4.2 ГГц',
          graphicCores: '8',
          graphicFrequency: '1750 МГц',
          cash: '12 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        },
        {
          name: 'Ryzen 7',
          model: '4700U',
          img: require('../assets/img/processors/ryzen7.png'),
          cores: '8/8',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '15 Вт',
          frequency: '4.1 ГГц',
          graphicCores: '7',
          graphicFrequency: '1600 МГц',
          cash: '12 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        },
        {
          name: 'Ryzen 5',
          model: '4600U',
          img: require('../assets/img/processors/ryzen5.png'),
          cores: '6/12',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '15 Вт',
          frequency: '4.0 ГГц',
          graphicCores: '6',
          graphicFrequency: '1500 МГц',
          cash: '11 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        },
        {
          name: 'Ryzen 5',
          model: '4500U',
          img: require('../assets/img/processors/ryzen5.png'),
          cores: '6/6',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '15 Вт',
          frequency: '4.0 ГГц',
          graphicCores: '6',
          graphicFrequency: '1500 МГц',
          cash: '11 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        },
        {
          name: 'Ryzen 3',
          model: '4300U',
          img: require('../assets/img/processors/ryzen3.png'),
          cores: '4/4',
          architecture: 'AMD «Zen 2» 7нм',
          tdp: '15 Вт',
          frequency: '3.7 ГГц',
          graphicCores: '5',
          graphicFrequency: '1400 МГц',
          cash: '6 МБ',
          interface: 'Wi-Fi 6, Bluetooth 5',
          display: 'До 4К с HDR'
        }
      ]
    }
  },
  computed: {
    itemsSliced() {
      //Делаем копию
      let tmp = JSON.parse(JSON.stringify(this.items));
      //Удаляем поля, использованные в заголовке, чтобы выводить ячейки в цикле только по остальным значениям
      for (let i=0; i < Object.keys(tmp).length; i++){
        delete tmp[i].name;
        delete tmp[i].img;
        delete tmp[i].model;
      }
      return tmp;
    }
  }
}
</script>

<style lang="stylus">
.processors-table
  padding 75px 0 50px
  position relative
  @media (max-width 1279px)
    padding 0
.table
  @media (max-width 1279px)
    padding-left 25%
    overflow-x scroll
    padding-bottom 20
    &::-webkit-scrollbar
      width 2px
    &::-webkit-scrollbar-track
      background var(--gray)
    &::-webkit-scrollbar-thumb
      background-color var(--accent)
      outline 0
  @media (max-width 767px)
    padding-left 50%
.tr
  display grid
  grid-template-columns 202px 100px 150px 85px 100px 85px 120px 120px 150px 150px
  grid-gap 2px
  margin-bottom 2px
  @media (max-width 1279px)
    display flex
  .td
    background: var(--gray)
    display flex
    justify-content center
    align-items center
    padding 0 20px
    line-height 1.2
    text-align center
    transition background-color .5s
    @media (max-width 1279px)
      flex-shrink 0
      width 25%
      min-height calc(12.5vw - 20px)
      font-size 14px
    @media (max-width 767px)
      min-height calc(25vw - 20px)
      width 100%
    &--title
      display grid
      grid-template-columns minmax(0,1fr) 1fr
      grid-gap 2px
      align-items center
      padding 0
      @media (max-width 1279px)
        position absolute
        left 20px
        width calc(25% - 22px)
      @media (max-width 767px)
        width calc(50% - 22px)
      img
        width 100%
        height auto
      span
        display block
        &:last-child
          color var(--accent)
  &:hover
    @media (hover)
      .td
        background-color #dedede !important

  &--th .td:first-child
    @media (max-width 1279px)
      position absolute
      left 0
      width 25%
      background #fff !important
    @media (max-width 767px)
      width 50%

  &:nth-child(odd)
    .td
      background: var(--gray2)
  &--th
    .td
      display flex
      align-items flex-end
      background none !important
      color var(--accent)
      font-size 12px
      font-weight bold
      justify-content center
      text-align center
      padding 10px 5px
</style>

<template>

  <div class="advantages__graphs">
    <h4 class="advantages__graph-title">{{ title }}</h4>
    <div v-for="(item,index) in counterCaption" :key="index" class="advantages__graph">
      <p>{{ item }}</p>
      <div class="advantages__graph-base">
        <div class="advantages__graph-value"
             :class="{ 'advantages__graph-value--target': isTarget[index] }"
             :style="graphWidth[index]">
          <span>{{ counterVal[index] }}</span>
        </div>
      </div>
    </div>
  </div>

</template>

<script>

export default {
  name: 'AdvantageGraph',
  props: ['title','counter','counterCaption','isTarget'],
  data: () => {
    return {
      counterVal: [],
      duration: 2000,
      startGraph: false,
      offsetTop: 0
    }
  },
  computed: {
    graphWidth: function() {
      // Устанавливаем width у графика
      let array = [];
      let max = Math.max.apply(Math, this.counter);
      for (let item of this.counter){
        let width = 100 * this.startGraph;
        if (item != max) width = width * item / max;
        array.push({
          width: width + '%'
        });
      }
      return array;
    }
  },
  watch: {
    offsetTop() {
      // Запускаем график, если он попал во viewport
        if (!this.startGraph && this.isElementInViewport(this.$el)) {
          this.startGraph = true;
          this.animateCounter();
        }
    }
  },
  methods: {
    onScroll() {
      // Проверяем скролл от верха документа
      this.offsetTop = window.pageYOffset || document.documentElement.scrollTop
    },
    isElementInViewport(el) {
      // Проверяем находится ли элемент во вьюпорте
      let rect = el.getBoundingClientRect();
      return (
          rect.top >= 0 &&
          rect.left >= 0 &&
          rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
          rect.right <= (window.innerWidth || document.documentElement.clientWidth)
      );
    },
    animateCounter() {
      // Анимируем счетчик
      let step = Math.ceil(Math.max.apply(Math, this.counter)/100);

      let stepTime = [];
      let timers = [];

      for (let i = 0; i < this.counter.length; i++) {

        stepTime.push(Math.floor(this.duration / this.counter[i] * step));
        this.counterVal.push(0);

        timers[i] = setInterval(() => {
          this.$set(this.counterVal, i, this.counterVal[i] + step);
          if (this.counterVal[i] >= this.counter[i]) {
            this.$set(this.counterVal, i, this.counter[i]);
            clearInterval(timers[i]);
          }
        }, stepTime[i]);

      }

    }
  },
  mounted: function () {
    // Начинаем следить за попаданием графиков во viewport
    window.addEventListener('scroll', this.onScroll);
  }
}

</script>

<style lang="stylus">
.advantages__graphs
  display flex
  flex-direction column-reverse
  margin-top 50px
  @media (max-width 1279px)
    margin-top 40px
.advantages__graph
  margin-bottom 30px
  font-size 18px
  font-family 'Uni', sans-serif
  text-transform uppercase
  @media (max-width 1279px)
    font-size 14px
    margin-bottom 20px
  &-title
    font-size 14px
    font-weight 400
    margin 0
    @media (max-width 1279px)
      font-size 12px
  p
    margin 0 0 10px
  &-base
    background var(--gray)
    display flex
  &-value
    text-align right
    background var(--gradient2)
    transition width 2s ease-in-out
    overflow-x hidden
    padding-top 3px
    span
      color #fff
      padding 0 15px
      line-height 25px
    &--target
      background var(--gradient)
</style>


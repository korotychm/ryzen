<template>

  <section class="laptops" id="laptops">

    <!-- Карточка товара -->
    <div class="popup" v-if="popupShown">
      <div class="popup__inner">
        <div class="popup__close" @click="popupShown = !popupShown"></div>
        <div class="card">
          <div class="gallery">
            <div class="gallery__nav">
              <div class="gallery__arrow gallery__arrow--prev" @click="prevSlide()"></div>
              <div class="gallery__arrow gallery__arrow--next" @click="nextSlide()"></div>
            </div>
            <div class="gallery__track">
              <div v-for="(src,index) in itemCard.gallery" :key="index" :class="{ 'gallery__slide--active': (slideIndex == index) }" class="gallery__slide">
                <img :src="src" alt=""/>
              </div>
            </div>
          </div>
          <div class="product">
            <h3 class="product__name">
              {{ itemCard.name }}
            </h3>
            <div class="product__info">
              <div>
                <h4>Процессор</h4>
                <p>{{ itemCard.processor }} {{ itemCard.model }}</p>
              </div>
              <div>
                <h4>Оперативная память</h4>
                <p>{{ itemCard.ram }} ГБ</p>
              </div>
              <div>
                <h4>Накопитель (SSD)</h4>
                <p>{{ itemCard.ssd }} ГБ</p>
              </div>
              <div>
                <h4>Диагональ экрана</h4>
                <p>{{ itemCard.display }}"</p>
              </div>
              <div>
                <h4>Видеокарта</h4>
                <p>{{ itemCard.graphics }}</p>
              </div>
              <div>
                <h4>Операционная система</h4>
                <p>{{ itemCard.os }}</p>
              </div>
            </div>
            <div class="product__buy">
              <div class="product__price">
                {{ itemCard.price.toLocaleString('ru')}} <span class="rub">₽</span>
              </div>
              <a class="btn btn--buy" :href="itemCard.link" target="_blank">Купить</a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="container">
      <h2 class="heading">Ноутбуки на базе <span class="heading__accent">AMD Ryzen</span></h2>
      <div class="catalog-panel">
        <div class="btn-group">
          <a class="btn"
             :class="{ 'btn--accent': !selectedCategory }"
             @click="selectedCategory=''"
          >
            Все ноутбуки
          </a>
          <a class="btn"
             v-for="(item,index) in categories"
             :key="index"
             :class="{ 'btn--accent': (selectedCategory == item) }"
             @click="selectedCategory=item"
          >
            {{ item }}
          </a>
        </div>
        <div class="sort">
          Сортировка
          <div class="sort__btn" @click="sortShown = !sortShown" :class="{ 'sort__btn--active': sortShown }">
            {{ sort }}
            <div class="sort__dropdown" :class="{ 'sort__dropdown--active': sortShown }">
              <label>
                <input type="radio"
                       name="sort"
                       value=""
                       v-model="sortKey"
                       @click="changeSort('По умолчанию')"
                       checked="checked"
                />
                <div class="sort__item">По умолчанию</div>
              </label>
              <label>
                <input type="radio"
                       name="sort"
                       value="price"
                       v-model="sortKey"
                       @click="changeSort('По цене')"
                />
                <div class="sort__item">По цене</div>
              </label>
              <label>
                <input type="radio"
                       name="sort"
                       value="processor"
                       v-model="sortKey"
                       @click="changeSort('По процессору')"
                />
                <div class="sort__item">По процессору</div>
              </label>
              <label>
                <input type="radio"
                       name="sort"
                       value="ram"
                       v-model="sortKey"
                       @click="changeSort('По памяти')"
                />
                <div class="sort__item">По памяти</div>
              </label>
              <label>
                <input type="radio"
                       name="sort"
                       value="ssd"
                       v-model="sortKey"
                       @click="changeSort('По накопителю')"
                />
                <div class="sort__item">По накопителю</div>
              </label>
              <label>
                <input type="radio"
                       name="sort"
                       value="display"
                       v-model="sortKey"
                       @click="changeSort('По диагонали')"
                />
                <div class="sort__item">По диагонали</div>
              </label>
            </div>
          </div>
        </div>
      </div>

      <div class="catalog">
        <div class="filter">
            <div class="filter__mobile-panel">
              <button class="filter__show" @click="filterShown = !filterShown"></button>
              <button class="filter__show filter__show--sort" @click="sortShown = !sortShown"></button>
            </div>
            <div class="filter__wrap" :class="{ 'filter__wrap--active': filterShown }">
              <div class="filter__close" @click="filterShown = !filterShown"></div>
              <h3>Подбери ноутбук</h3>
              <div class="filter__item">
                <h4>Цена</h4>
                <div class="range">
                  <input class="range__left"
                         type="range"
                         :min="min"
                         :max="max"
                         step="1"
                         v-model.number="minPrice"
                  />
                  <input class="range__right"
                         type="range"
                         :min="min"
                         :max="max"
                         step="1"
                         v-model.number="maxPrice"
                  />
                  <div class="range__slider">
                    <div class="range__track"></div>
                    <div :style="[leftRangeStyle, rightRangeStyle]" class="range__range"></div>
                    <div :style="leftRangeStyle" class="range__thumb range__thumb--left"></div>
                    <div :style="rightRangeStyle" class="range__thumb range__thumb--right"></div>
                  </div>
                  <div class="range__tooltips">
                    <input type="number" v-model.lazy="minPrice"/>
                    <input type="number" v-model.lazy="maxPrice"/>
                  </div>
                </div>
              </div>

              <div class="filter__item" v-for="(filter,index) in filterValues" :key="index">
                <h4>{{ filter.name }}</h4>
                <div class="filter__checks">
                  <label v-for="(val,key) in filter.values" :key="key" class="filter__check">
                    <input type="checkbox"
                           :value="val"
                           @click="checkFilter(index, val)"
                    />
                    <div class="check"></div>
                    {{ val }}{{ filter.unit }}
                  </label>
                </div>
              </div>

              <button class="btn btn--accent" @click="filterShown=!filterShown">Применить фильтры</button>

            </div>
        </div>

        <div v-if="filteredItems.length" class="catalog__items">

          <div v-for="product in filteredItems" :key="product.id" class="product">
            <div class="product__img" @click="popupItem(product.id)">
              <img width="219" height="130" :src="product.img" alt=""/>
            </div>
            <h3 class="product__name">
              {{ product.name }}
            </h3>
            <div class="product__info">
              <div>
                <h4>Процессор</h4>
                <p>{{ product.processor }} {{ product.model }}</p>
              </div>
              <div>
                <h4>Оперативная память</h4>
                <p>{{ product.ram }} ГБ</p>
              </div>
              <div>
                <h4>Накопитель (SSD)</h4>
                <p>{{ product.ssd }} ГБ</p>
              </div>
              <div>
                <h4>Диагональ экрана</h4>
                <p>{{ product.display }}"</p>
              </div>
              <div>
                <h4>Видеокарта</h4>
                <p>{{ product.graphics }}</p>
              </div>
              <div>
                <h4>Операционная система</h4>
                <p>{{ product.os }}</p>
              </div>
            </div>
            <div class="product__buy">
              <div class="product__price">
                {{ product.price.toLocaleString('ru')}} <span class="rub">₽</span>
              </div>
              <a class="btn btn--buy" :href="product.link" target="_blank">Купить</a>
            </div>
          </div>

        </div>
        <div class="catalog__empty" v-else>Ничего не найдено, попробуйте задать другие фильтры для поиска.</div>
      </div>
    </div>
  </section>

</template>

<script>
export default {
  name: 'Laptops',
  data: () => {
    return {
      items: [
        {
          id: 1,
          name: 'Asus M433IA-EB005T',
          make: 'Asus',
          price: 59890,
          img: require('../assets/img/laptops/laptop1.jpg'),
          gallery: [require('../assets/img/laptops/laptop1.jpg'),require('../assets/img/laptops/laptop2.jpeg'),require('../assets/img/laptops/laptop3.jpeg')],
          processor: 'Ryzen 5',
          model: '4500U',
          ram: 8,
          ssd: 256,
          display: 14,
          graphics: 'Radeon Graphics',
          os: 'Win10',
          category: 'Ультралегкие',
          link: 'https://citilink.ru/'
        },
        {
          id: 2,
          name: 'Acer Aspire 5 A515-44-R8F8',
          make: 'Acer',
          price: 48999,
          img: require('../assets/img/laptops/laptop2.jpeg'),
          processor: 'Ryzen 5',
          model: '4500U',
          ram: 8,
          ssd: 256,
          display: 15.6,
          graphics: 'Radeon Graphics',
          os: 'Linux',
          category: 'Ультралегкие',
          link: 'https://citilink.ru/'
        },
        {
          id: 3,
          name: 'Asus ROG Zephyrus G14 GA401IU-HE094T',
          make: 'Asus',
          price: 114999,
          img: require('../assets/img/laptops/laptop3.jpeg'),
          processor: 'Ryzen 7',
          model: '4800HS',
          ram: 16,
          ssd: 512,
          display: 14,
          graphics: 'GeForce GTX1660Ti',
          os: 'Win10',
          category: ['Ультралегкие','Игровые'],
          link: 'https://citilink.ru/'
        },
        {
          id: 4,
          name: 'HP Envy x360 13-ay0002ur 1Y8K8EA',
          make: 'HP',
          price: 64990,
          img: require('../assets/img/laptops/laptop4.jpeg'),
          processor: 'Ryzen 5',
          model: '4500U',
          ram: 8,
          ssd: 256,
          display: 13.3,
          graphics: 'Radeon Graphics',
          os: 'Win10',
          category: 'Ультралегкие',
          link: 'https://citilink.ru/'
        },
        {
          id: 5,
          name: 'HP Omen 15-en0020ur 1U3C8EA',
          make: 'HP',
          price: 89990,
          img: require('../assets/img/laptops/laptop5.jpeg'),
          processor: 'Ryzen 7',
          model: '4800H',
          ram: 16,
          ssd: 512,
          display: 15.6,
          graphics: 'GeForce GTX1660Ti',
          os: 'Win10',
          category: ['Игровые'],
          link: 'https://citilink.ru/'
        },
        {
          id: 6,
          name: 'Lenovo IdeaPad 3 15ARE05',
          make: 'Lenovo',
          price: 43999,
          img: require('../assets/img/laptops/laptop6.jpeg'),
          processor: 'Ryzen 3',
          model: '4300U',
          ram: 8,
          ssd: 512,
          display: 15.6,
          graphics: 'Radeon Graphics',
          os: 'DOS',
          category: 'Ультралегкие',
          link: 'https://citilink.ru/'
        },
        {
          id: 7,
          name: 'Lenovo IdeaPad 5 14ARE05',
          make: 'Lenovo',
          price: 43999,
          img: require('../assets/img/laptops/laptop7.jpeg'),
          processor: 'Ryzen 3',
          model: '4300U',
          ram: 8,
          ssd: 512,
          display: 14,
          graphics: 'Radeon Graphics',
          os: 'DOS',
          category: 'Ультралегкие',
          link: 'https://citilink.ru/'
        },
        {
          id: 8,
          name: 'Asus VivoBook S14 M433IA-EB579T',
          make: 'Asus',
          price: 49999,
          img: require('../assets/img/laptops/laptop8.jpeg'),
          processor: 'Ryzen 3',
          model: '4300U',
          ram: 8,
          ssd: 256,
          display: 14,
          graphics: 'Radeon Graphics',
          os: 'Win10',
          category: 'Ультралегкие',
          link: 'https://citilink.ru/'
        }
      ],
      categories: ['Ультралегкие','Игровые'],
      filters: [
        {
          name: 'Производитель',
          key: 'make'
        },
        {
          name: 'Процессор',
          key: 'processor'
        },
        {
          name: 'Оперативная память',
          key: 'ram',
          unit: ' ГБ'
        },
        {
          name: 'Накопитель SSD',
          key: 'ssd',
          unit: ' ГБ'
        },
        {
          name: 'Диагональ экрана',
          key: 'display',
          unit: '"'
        },
        {
          name: 'Операционная система',
          key: 'os'
        }
      ],
      minPrice: 0,
      maxPrice: 1000000,
      selectedCategory: '',
      sortShown: false,
      sort: 'По умолчанию',
      sortKey: '',
      filterShown: false,
      currentItem: 1,
      popupShown: false,
      slideIndex: 0
    }
  },
  computed: {
    itemCard: function() {
      //Находим текущий товар в items
      let item = this.items.filter(obj => {
        return obj.id === this.currentItem
      });
      return item[0];
    },
    filteredItems: function() {
      // Фильтруем каталог по цене
      let tmp = this.items.filter(item => (item.price >= this.minPrice && item.price <= this.maxPrice) ? item : '');
      // Фильтруем каталог по категории
      if (this.selectedCategory) {
        tmp = tmp.filter(item => (item.category == this.selectedCategory || item.category.includes(this.selectedCategory)) ? item : '');
      }
      // Фильтруем каталог по фильтрам
      for (let filter of this.filters) {
        if (filter.selected.length){
          tmp = tmp.filter(item => (filter.selected.includes(item[filter.key])) ? item : '');
        }
      }
      // Сортируем каталог
      if (this.sortKey){
        tmp.sort((a, b) => a[this.sortKey] > b[this.sortKey] ? 1 : -1);
      }
      return tmp;
    },
    filterValues: function() {
      // Ищем уникальные значения для фильтров
      let filters = [...this.filters];
      for (let filter of filters) {
        filter.values = [];
        this.$set(filter, 'selected', []);
        for (let item of this.items) {
          // Eсли не содержит такое значение - добавляем
          if (!filter.values.includes(item[filter.key])){
            filter.values.push(item[filter.key]);
          }
        }
        filter.values.sort();
      }
      return filters;
    },
    min: function() {
      // Минимальная цена
      return this.getMinPrice();
    },
    max: function() {
      // Максимальная цена
      return this.getMaxPrice();
    },
    leftRangeStyle: function() {
      // Присваиваем left слайдеру
      let min = this.getMinPrice(),
          max = this.getMaxPrice();
      let percent = (this.minPrice - min) / (max - min) * 100;
      return {
        left: percent + '%'
      }
    },
    rightRangeStyle: function() {
      // Присваиваем right слайдеру
      let min = this.getMinPrice(),
          max = this.getMaxPrice();
      let percent = (this.maxPrice - min) / (max - min) * 100;
      return {
        right: 100 - percent + '%'
      }
    }
  },
  watch: {
    minPrice() {
      this.checkRange();
    },
    maxPrice() {
      this.checkRange();
    }
  },
  methods: {
    nextSlide() {
      // Следующий слайд
      if ((this.slideIndex + 1) == this.itemCard.gallery.length) {
        this.slideIndex = 0;
      } else {
        this.slideIndex++;
      }
    },
    prevSlide() {
      // Предыдущий слайд
      if (this.slideIndex == 0) {
        this.slideIndex = this.itemCard.gallery.length - 1;
      } else {
        this.slideIndex--;
      }
    },
    popupItem(id) {
      this.currentItem = id;
      // Показываем попап с карточкой товара
      this.popupShown = true;
      // Устанавливаем первый слайд активным
      this.slideIndex = 0;
    },
    changeSort(value) {
      // Меняем текущий текст селекта сортировки и закрываем
      this.sort = value;
      this.sortShown = !this.sortShown;
    },
    checkFilter(index, value) {
      // Добавляем выбранные фильтры или убираем
      let arr = this.filters[index].selected;
      if (arr.includes(value)){
        let i = arr.indexOf(value);
        if (index !== -1) {
          arr.splice(i, 1);
        }
      } else {
        arr.push(value);
      }
      this.$set(this.filters[index], 'selected', arr);
    },
    checkRange() {
      // Проверяем является ли значение инпутов числом
      if (typeof(this.maxPrice) != 'number'){
        this.maxPrice = this.getMaxPrice();
      }
      if (typeof(this.minPrice) != 'number'){
        this.minPrice = this.getMinPrice();
      }
      // Проверяем чтобы значения инпутов соответствовали минимальной и максимальной в товарах
      if (this.minPrice < this.getMinPrice()){
        this.minPrice = this.getMinPrice();
      }
      if (this.maxPrice > this.getMaxPrice()){
        this.maxPrice = this.getMaxPrice();
      }
      // Проверяем чтобы минимальная цена не была больше максимальной и наоборот
      if (this.minPrice > this.maxPrice){
        let tmp = this.maxPrice;
        this.maxPrice = this.minPrice;
        this.minPrice = tmp;
      }
    },
    setStartRangeValues() {
      //Устанавливаем начальные значения слайдера цены
      this.minPrice = this.getMinPrice();
      this.maxPrice = this.getMaxPrice();
    },
    getMinPrice() {
      //Получаем минимальную цену товаров
      return this.items.reduce(function(prev, curr) {
        return prev.price < curr.price ? prev : curr;
      }).price;
    },
    getMaxPrice() {
      //Получаем максимальную цену товаров
      return this.items.reduce(function(prev, curr) {
        return prev.price > curr.price ? prev : curr;
      }).price;
    }
  },
  mounted: function () {
    //Устанавливаем начальные значения слайдера цены
    this.setStartRangeValues();
  }
}
</script>

<style lang="stylus">

.popup
  position fixed
  background rgba(0,0,0,.6)
  width 100vw
  height 100vh
  left 0
  top 0
  display flex
  align-items center
  justify-content center
  z-index 10
  &__inner
    background #fff
    padding 40px
    position relative
    @media (max-width: 767px)
      width 100vw
      padding 0
  &__close
    display flex
    width 40px
    height 40px
    background var(--accent)
    position absolute
    top 0
    right 0
    z-index 10
    cursor pointer
    &::before
    &::after
      content ''
      position absolute
      display block
      width 25px
      height 3px
      background #fff
      top 50%
      left 50%
      transform translate(-50%,-50%) rotate(45deg)
    &::after
      transform translate(-50%,-50%) rotate(-45deg)



.catalog-panel
  display flex
  justify-content space-between
  align-items center
.sort
  display flex
  align-items center
  @media (max-width 767px)
    position absolute
    background #fff
    font-size 0
    z-index 10
    right 20px
    top 240px
  &__btn
    border 3px solid #000
    padding 7px 15px
    margin-left 20px
    width 227px
    cursor pointer
    position relative
    user-select none
    @media (max-width 1023px)
      margin-left 15px
      width 180px
    @media (max-width 767px)
      font-size 14px
      display none
      &--active
        display block
    &::after
      content ''
      display block
      width 10px
      height 10px
      border-right 2px solid #000
      border-bottom 2px solid #000
      transform rotate(45deg)
      position absolute
      right 10px
      top 9px
  &__item
    padding 7px 15px
    border-bottom 3px solid #000
    cursor pointer
    transition background-color .5s
    &:hover
      @media (hover)
        background var(--gray2)
  &__dropdown
    position absolute
    z-index 10
    background #fff
    border 3px solid #000
    border-bottom none
    width calc(100% + 6px)
    left -3px
    bottom 0
    transform translateY(100%)
    display none
    &--active
      display block
    input
      display none
      &:checked + .sort__item
        color #fff
        background var(--accent)


.product
  padding-bottom 30px
  border 2px solid var(--accent)
  background #fff
  @media (max-width 1023px)
    padding-bottom 15px
  &__buy
    padding 0 20px
    display flex
    align-items center
    justify-content space-between
    @media (max-width 1023px)
      display block
      padding 0 15px
      .btn
        width 100%
        text-align center
  &__price
    font-family 'Uni', sans-serif
    font-size 21px
    @media (max-width 1023px)
      font-size 18px
      margin-bottom 10px
      text-align center
    .rub
      font-family 'Noto', sans-serif
      font-style italic
      font-size 16px
      font-weight 400
      position relative
      bottom 1px
  &__info
    padding 0 20px
    margin 15px 0 30px
    @media (max-width 1023px)
      padding 0 15px
      margin-bottom 15px
    div
      border-bottom 2px solid var(--accent)
      padding-bottom 5px
      margin-bottom 8px
    h4
      font-size 10px
      letter-spacing .3px
      font-weight normal
      margin 0 0 5px
      @media (max-width 1023px)
        font-size 8px
        margin-bottom 2px
    p
      margin 0
      font-size 14px
      @media (max-width 1023px)
        font-size 12px
  &__img
    padding 30px 0
    display flex
    justify-content center
    align-items center
    cursor pointer
    position relative
    @media (max-width 1023px)
      padding 15px 0
    &::after
      content ''
      width 30px
      height 30px
      display block
      background var(--accent)
      background-image url('../assets/img/laptops/search.svg')
      background-repeat no-repeat
      background-position center
      position absolute
      top -2px
      right -2px
      transition background-size .5s ease-in-out, background-color .5s ease-in-out, width .5s ease-in-out, height .5s ease-in-out
    &:hover::after
      @media(hover)
        width calc(100% + 2px)
        height calc(100% + 50px)
        background-color rgba(255,125,0,.1)
        background-size 20%
    img
      width 100%
      height 130px
      object-fit contain
      @media (max-width 1023px)
        height 100px
  &__name
    margin 0
    font-size 16px
    font-weight bold
    color var(--accent)
    min-height 45px
    padding 0 20px
    @media (max-width 1023px)
      padding 0 15px
      font-size 12px
      min-height 35px

.laptops
  padding 50px 0 0
  @media (max-width 1279px)
    padding-top 100px
  @media (max-width 767px)
    padding-top 50px
  .heading
    margin 0 0 40px
  .btn-group
    @media (max-width 767px)
      flex-wrap nowrap
      overflow-x scroll
    .btn
      font-size 12px
      margin-right 10px
      flex-shrink 0

.catalog
  display grid
  grid-template-columns 200px calc(100% - 280px)
  grid-gap 80px
  margin-top 50px
  align-items flex-start
  min-height 1250px
  @media (max-width 767px)
    min-height 0
    display block
    margin-top 30px
  &__items
    display grid
    grid-template-columns 1fr 1fr 1fr 1fr
    grid-gap 30px
    @media (max-width 1279px)
      grid-template-columns minmax(0,1fr) minmax(0,1fr)
      grid-gap 15px

.filter
  @media (max-width 767px)
    display block
    width 100%
    margin-bottom 20px
  h3
    font-family 'Uni', sans-serif
    text-transform uppercase
    margin 0
    font-size 18px
  &__mobile-panel
    display none
    @media (max-width 767px)
      display flex
      justify-content space-between
      height 40px
  &__show
    width 30px
    height 30px
    padding 0
    background url('../assets/img/laptops/filter.svg') no-repeat center
    background-size contain
    position relative
    &::after
      content 'Фильтр'
      display block
      position absolute
      right -55px
      top 7px
    &--sort
      background url('../assets/img/laptops/sort.svg') no-repeat center
      &::after
        content 'Сортировка'
        right 0
        left -122px
  &__close
    display none
    @media (max-width 767px)
      display flex
      width 60px
      height 60px
      background var(--accent)
      position fixed
      top 0
      right 0
      z-index 10
      &::before
      &::after
        content ''
        position absolute
        display block
        width 25px
        height 3px
        background #fff
        top 50%
        left 50%
        transform translate(-50%,-50%) rotate(45deg)
      &::after
        transform translate(-50%,-50%) rotate(-45deg)
  &__wrap
    .btn
      display none
    @media (max-width 767px)
      display none
      position fixed
      top 0
      left 0
      width 100vw
      height 100vh
      background #fff
      z-index 10
      overflow-y auto
      padding 30px 20px 200px
      &--active
        display block
      &::after
      &::after
        content ''
        display block
        width 100vw
        height 150px
        background: #fff;
        position fixed
        bottom 0
        left 0
        border-top 2px solid var(--accent)
      .btn
        display inline-flex
        position fixed
        bottom 50px
        left 50%
        transform translateX(-50%)

  &__item
    margin-bottom 25px
    h4
      font-size 16px
      font-weight bold
      margin 40px 0 15px
  &__check
    display block
    position relative
    font-size 14px
    line-height 20px
    padding-left 28px
    margin-bottom 8px
    cursor pointer
    &--disabled
      pointer-events none
      opacity .5
    .check
      position absolute
      top 0
      left 0
      width 20px
      height 20px
      border 2px solid var(--accent)
      padding 3px
    input
      display none
      &:checked + .check::after
        content ''
        display block
        width 100%
        height 100%
        background var(--accent)


.range
  margin-top 25px
  position relative
  width 100%
  &__tooltips
    display flex
    justify-content space-between
    margin-top 20px
    input
      width 65px
      height 30px
      background var(--gray)
      font-size 12px
      border none
      text-align center
      -moz-appearance textfield
      &::-webkit-outer-spin-button
      &::-webkit-inner-spin-button
        -webkit-appearance none
        margin 0
      &:focus
        outline none
        border 2px solid var(--accent)
  input[type="range"]
    position absolute
    -webkit-appearance none
    z-index 2
    height 5px
    width 100%
    margin-top 0
    opacity 0
    pointer-events none
    &::-webkit-slider-thumb
      pointer-events all
      width 20px
      height 20px
      border-radius 0
      border none
      -webkit-appearance none
      cursor pointer
  &__slider
    position relative
    z-index 1
    height 5px
    margin 0 10px
  &__track
    position absolute
    z-index 1
    left 0
    right 0
    top 0
    bottom 0
    border-radius 5px
    background-color var(--gray)
  &__range
    position absolute
    z-index 2
    left 25%
    right 25%
    top 0
    bottom 0
    border-radius 5px
    background-color var(--accent)
    opacity .5
  &__thumb
    position absolute
    z-index 3
    width 20px
    height 20px
    background-color var(--accent)
    border-radius 50%
    transition box-shadow .3s ease-in-out
    &--left
      left 25%
      transform translate(-10px, -8px)
    &--right
      right 25%
      transform translate(10px, -8px)

  &__left:hover ~ .range__slider .range__thumb--left
  &__right:hover ~ .range__slider .range__thumb--right
    @media (hover)
      box-shadow 0 0 0 10px rgba(255,125,0,.1)
  &__left:active ~ .range__slider .range__thumb--left
  &__right:active ~ .range__slider .range__thumb--right
    box-shadow 0 0 0 20px rgba(255,125,0,.2)

.card
  display flex
  width 100%
  .product
    margin-left 30px
    width 250px
    padding-top 30px
    @media (max-width: 1279px)
      width 220px
    @media (max-width: 1023px)
      width 170px
    @media (max-width: 767px)
      display none
  .gallery
    width 600px
    overflow hidden
    position relative
    @media (max-width: 1279px)
      width 500px
    @media (max-width: 767px)
      width 100%
      height 500px

    &__nav
      display flex
      justify-content space-between
      width 100%
      position absolute
      top 50%
      transform translateY(-50%)
      left 0
      pointer-events none
      z-index: 3
    &__arrow
      width 60px
      height 60px
      border 3px solid var(--accent)
      border-radius 50%
      background transparent
      padding-top 16px
      padding-left 10px
      transition opacity .5s, border-color .5s
      pointer-events auto
      background #fff
      cursor pointer
      touch-action manipulation
      &::after
        content ''
        width 20px
        height 20px
        display block
        border-right 3px solid var(--accent)
        border-bottom 3px solid var(--accent)
        transform: rotate(-45deg)
        transition border-color .5s
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
    &__track
      display block
      position relative
      height 100%
    &__slide
      position absolute
      top 50%
      left 50%
      transform translate(-50%,-50%)
      opacity 0
      transition opacity .5s ease-in-out
      z-index 1
      @media (max-width: 767px)
        width 80%
      &--active
        opacity 1
        z-index 2
      img
        width 500px
        height 100%
        object-fit contain
        @media (max-width: 1279px)
          width 400px
        @media (max-width: 767px)
          width 100%
</style>

<template>
  <div class="mt-1">
    <h3>Пицца</h3>
    <div class="product--list d-flex">
      <div
        v-for="item in recom"
        :key="item.id"
        class="product--item d-flex"
        @click="$bvModal.show(`modal-xl-${item.id}`)"
      >
        <img :src="item.img" :alt="item.title" />
        <div>
          <span class="title"
            ><b>{{ item.title }}</b></span
          >
          <span class="product--item--description">
            {{ item.description.substring(0, 50) }}...
          </span>
          <span class="price">
            от {{ item.price }} &#8399;
            <small style="color: #b2b2b2">/ 360г</small></span
          >
          <div class="btn-select">Выбрать</div>
          <DetailProd
            :index="`modal-xl-${item.id}`"
            :item="item"
            @add-order="addOrder"
          />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Vue from 'vue'
import { ButtonPlugin } from 'bootstrap-vue'
import DetailProd from '~/components/Modals/DetailProd'

Vue.component('DetailProd', DetailProd)
Vue.use(ButtonPlugin)

export default {
  data() {
    return {
      sizeSelected: 0,
      sizeOptions: [
        { text: 'Маленькая (24 см, 360г.)', value: 0, price: 0 },
        { text: 'Средняя (30 см, 540г.)', value: 15, price: 15 },
        { text: 'Большая (34 см, 710г.)', value: 30, price: 30 },
      ],
      additionalProduct: [], // Must be an array reference!
      additionalOptions: [
        { text: 'Бекон', value: 'bacon', price: 56 },
        { text: 'Сырный бортик', value: 'cheese_side', price: 169 },
        { text: 'Ветчина', value: 'ham', price: 44 },
        { text: 'Грибы', value: 'mushrooms', price: 34 },
        { text: 'Острый халапеньо', value: 'spicy_jalapeno', price: 34 },
      ],
      recom: [
        {
          id: 1,
          quantity: 1,
          absolute_price: 0,
          title: 'Неополитана',
          price: 456,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/26fa2948b6c74113afb9d09a3262fc26_366x366.jpeg',
          description:
            'Пикантная пепперони, увеличенная порция моцареллы, томатный соус',
        },
        {
          id: 2,
          quantity: 1,
          absolute_price: 0,
          title: 'Маргарита',
          price: 599,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/e8a8ded1f8154d11ab5065dc5208b187_366x366.jpeg',
          description:
            'Увеличенная порция моцареллы, томаты, итальянские травы, томатный соус',
        },
        {
          id: 3,
          quantity: 1,
          absolute_price: 0,
          title: 'Цыпленок блю чиз',
          price: 475,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/fd490c30efa74d3ba137a9326594a4e5_366x366.jpeg',
          description:
            'Цыпленок, сыр блю чиз, томаты, моцарелла, соус альфредо',
        },
        {
          id: 4,
          quantity: 1,
          absolute_price: 0,
          title: 'Чизбургер-пицца',
          price: 450,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/Pizza/ru-RU/dc5dc4e9-932a-4abf-9472-dfb6326ea9ee.jpg',
          description:
            'Мясной соус болоньезе, соус бургер, соленые огурчики, томаты, красный лук, моцарелла',
        },
        {
          id: 5,
          quantity: 1,
          absolute_price: 0,
          title: 'Морская',
          price: 700,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/Pizza/ru-RU/8b052931-395f-4b38-8af0-55f6fbd7c9e5.jpg',
          description:
            'Пикантная пепперони, увеличенная порция моцареллы, томатный соус',
        },
        {
          id: 6,
          quantity: 1,
          absolute_price: 0,
          title: 'Супермясная',
          price: 648,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/Pizza/ru-RU/8b052931-395f-4b38-8af0-55f6fbd7c9e5.jpg',
          description:
            'Пикантная пепперони, цыпленок, острая чоризо, бекон, митболы из говядины, моцарелла, томатный соус',
        },
        {
          id: 7,
          quantity: 1,
          absolute_price: 0,
          title: 'Пепперони-сердце',
          price: 800,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/Pizza/ru-RU/4a041cbf-a02a-4d6f-a820-aa2005e25c4e.jpg',
          description: 'Пикантная пепперони, моцарелла, томатный соус',
        },
        {
          id: 8,
          quantity: 1,
          absolute_price: 0,
          title: 'Четыре сезона',
          price: 680,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/Pizza/ru-RU/6d4e1c2c-1c81-40c6-95d9-0d19afcebcb5.jpg',
          description:
            'Увеличенная порция моцареллы, ветчина, пикантная пепперони, кубики брынзы, томаты, шампиньоны, томатный соус, итальянские травы',
        },
      ],
      sumAdditional: null,
    }
  },
  mounted() {},
  methods: {
    addOrder(pizza) {
      this.$emit('add-order', pizza)
    },
  },
}
</script>
<style scoped>
.product--list {
  flex-wrap: wrap;
  margin-bottom: 100px;
  justify-content: space-between;
}
.product--item {
  width: 25%;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.product--item img {
  width: 200px;
  height: 200px;
}
.product--item div span {
  font-size: 14px;
}
.product--item--description {
  color: rgb(141, 142, 143);
  font-size: 14px;
  height: 60px;
  overflow: hidden; /* Обрезаем содержимое */
}
.product--item div {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  font-size: 30px;
  margin-left: 15px;
}
.price {
  font-size: 18px !important;
}
.title {
  font-size: 24px !important;
}
</style>

<template>
  <div>
    <div class="row d-flex header mt-3 align-items-center">
      <img
        src="https://webdozerz.github.io/pages/pizza/images/logo.svg"
        class="col-1"
        alt=""
      />
      <ul class="d-flex col-9">
        <li>Пицца</li>
        <li>Комбо</li>
        <li>Закуски</li>
        <li>Десерты</li>
        <li>Напитки</li>
        <li>Другие товары</li>
        <li>Акции</li>
        <li>Контакты</li>
        <li>О нас</li>
      </ul>
      <div id="show-btn" class="col-2 btn-select" @click="showModal">
        <b-icon-cart-plus /> {{ order.length }} шт.
      </div>
    </div>
    <b-modal ref="my-modal" hide-footer title="Ваш заказ">
      <div class="d-block">
        <div v-for="item in order" :key="item.id" class="product-order">
          <div>
            <img :src="item.img" :alt="item.title" />
            <span>{{ item.title }}</span>
          </div>
          <div>
            <span
              ><b>{{ item.price * item.quantity }} &#8399;</b></span
            >
            <b-form-spinbutton
              id="sb-inline"
              v-model="item.quantity"
              min="1"
              max="100"
              inline
              @change="totalPrice"
            ></b-form-spinbutton>
            <b-icon-trash2-fill color="#DC143C" style="margin-left: 10px" />
          </div>
        </div>
        <hr />
        <div class="total-price">Всего: {{ total_price }} руб.</div>
      </div>
    </b-modal>
  </div>
</template>
<script>
import Vue from 'vue'
import { ButtonPlugin, IconsPlugin, FormSpinbuttonPlugin } from 'bootstrap-vue'

Vue.use(FormSpinbuttonPlugin)
Vue.use(IconsPlugin)
Vue.use(ButtonPlugin)
export default {
  props: {
    order: {
      type: Array,
      require: false,
      default: () => {
        return []
      },
    },
  },
  data() {
    return {
      total_price: 0,
    }
  },
  watch: {
    order() {
      this.totalPrice()
    },
  },
  methods: {
    totalPrice() {
      let sum = 0
      this.order.forEach((element) => {
        element.absolute_price = element.price * element.quantity
      })
      this.order.forEach((price) => {
        // this.total_price = this.total_price + price.absolute_price
        sum = sum + price.absolute_price
        this.total_price = sum
      })
    },
    showModal() {
      this.$refs['my-modal'].show()
    },
    hideModal() {
      this.$refs['my-modal'].hide()
    },
    toggleModal() {
      this.$refs['my-modal'].toggle('#toggle-btn')
    },
  },
}
</script>
<style lang="scss" scoped>
.header {
  align-items: center;
}
.header ul li {
  margin-left: 31px;
  font-size: 1em;
}
.header ul li:hover {
  color: orangered;
  cursor: pointer;
  transition: 0.5s;
}
.product-order {
  display: flex;
  width: 100%;
  align-items: center;
  margin-top: 5px;
  padding: 1%;
  div {
    width: 50%;
  }
  img {
    width: 50px;
    height: 50px;
  }
  span {
    margin-left: 10px;
    margin-right: 10px;
  }
}
</style>

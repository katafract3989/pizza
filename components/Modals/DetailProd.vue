<template>
  <div>
    <b-modal ref="pizza-detail-modal" :id="index" hide-footer>
      <template #modal-title>
        {{ item.title }}
      </template>

      <div class="d-flex flex-wrap-wrap">
        <div class="preview-descr">
          <img :src="item.img" width="200px" height="200px" :alt="item.title" />
          <span>{{ item.description }}</span>
        </div>
        <div>
          <div class="additional-products">
            <div
              v-for="elem in additionalOptions"
              :key="elem.text"
              class="d-flex"
            >
              <span
                ><input
                  v-model="additionalProduct"
                  type="checkbox"
                  name="a"
                  :value="elem"
                />{{ elem.text }} +{{ elem.price }} руб.</span
              >
            </div>
          </div>
          <hr />
          <div class="size--products">
            <b-form-group>
              <b-form-radio-group
                id="radio-group-1"
                v-model="sizeSelected"
                :options="sizeOptions"
                name="radio-options"
              ></b-form-radio-group>
            </b-form-group>
          </div>
          <div class="add">
            <div class="btn-select" @click="addOrder">
              <b-icon-cart-plus /> Добавить в корзина за
              {{ totalPrice(item.price) }} &#8399;
            </div>
          </div>
        </div>
      </div>
    </b-modal>
  </div>
</template>
<script>
import Vue from 'vue'
import {
  IconsPlugin,
  ButtonPlugin,
  FormCheckboxPlugin,
  FormRadioPlugin,
  BFormRadioGroup,
  FormGroupPlugin,
} from 'bootstrap-vue'

import * as _ from 'lodash'

Vue.use(IconsPlugin)
Vue.use(FormGroupPlugin)
Vue.component('b-form-radio-group', BFormRadioGroup)
Vue.use(FormRadioPlugin)
Vue.use(FormCheckboxPlugin)
Vue.use(ButtonPlugin)
export default {
  props: {
    index: {
      type: String,
      require: false,
      default: '',
    },
    item: {
      type: Object,
      require: false,
      default: () => {
        return {}
      },
    },
  },
  data() {
    return {
      pizza: null,
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
      sumAdditional: null,
    }
  },
  watch: {
    additionalProduct() {
      this.totalPrice()
    },
    sizeSelected() {
      this.totalPrice()
    },
  },
  mounted() {},
  methods: {
    totalPrice(price = null) {
      let additionalSum = _.cloneDeep(this.sumAdditional)
      this.currentPrice = price
      this.additionalProduct.forEach(function (elem) {
        additionalSum = additionalSum + elem.price
      })
      const coefficient = _.cloneDeep(this.sizeSelected)
      this.pizza = { ...this.item }
      const procent = (this.currentPrice / 100) * coefficient
      return price + additionalSum + Math.round(procent)
    },
    addOrder() {
      this.$emit('add-order', this.pizza)
      this.$refs['pizza-detail-modal'].hide()
    },
  },
}
</script>

<style lang="scss">
.preview-descr {
  font-size: 14px;
  margin-right: 10px;
  width: 300px;
}
.size--products {
  font-size: 12px;
}
.additional-products {
  margin-top: 10px;
}
.additional-products input {
  margin-right: 10px;
}
.add {
  display: flex;
  padding: 10px;
  font-size: 14px;
  width: 100%;
}
.add-btn {
  padding: 10px;
  background: rgb(232, 97, 0);
  color: #fff;
  text-align: center;
  border-radius: 5px;
  cursor: pointer;
}
</style>

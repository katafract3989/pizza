<template>
  <div class="container">
    <Header :order="order" />
    <Slider />
    <Recommended />
    <hr />
    <Products @add-order="addOrder" />
  </div>
</template>

<script>
export default {
  components: {
    Header: () => import('~/components/Pages/Header'),
    Slider: () => import('~/components/Pages/Slider'),
    Recommended: () => import('~/components/Pages/Recommended'),
    Products: () => import('~/components/Pages/Products'),
  },
  data() {
    return {
      order: [],
    }
  },
  mounted() {},
  methods: {
    addOrder(pizza) {
      const id = pizza.id
      if (this.order.length !== 0) {
        this.order.forEach((elem) => {
          if (!elem.id === id) this.order.push(pizza)
        })
      } else {
        this.order.push(pizza)
      }
    },
  },
}
</script>

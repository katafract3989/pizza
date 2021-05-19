<template>
  <div class="mt-3">
    <h3>Очень вкусно! Клиенты выбирают</h3>
    <div class="recommended--list d-flex">
      <div
        v-for="item in recom"
        :key="item.id"
        class="recommended--item d-flex col-3"
      >
        <img :src="item.img" width="100px" height="100px" alt="" />
        <div>
          <span
            ><b>{{ item.title }}</b></span
          >
          <span> от {{ item.price }} &#8399; </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      recom: [
        {
          id: 1,
          title: 'Неополитана',
          price: 456,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/26fa2948b6c74113afb9d09a3262fc26_366x366.jpeg',
          description:
            'Пикантная пепперони, увеличенная порция моцареллы, томатный соус',
        },
        {
          id: 2,
          title: 'Цезарь',
          price: 599,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/e8a8ded1f8154d11ab5065dc5208b187_366x366.jpeg',
          description:
            'Пикантная пепперони, увеличенная порция моцареллы, томатный соус',
        },
        {
          id: 3,
          title: 'Биг-чиз',
          price: 475,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/fd490c30efa74d3ba137a9326594a4e5_366x366.jpeg',
          description:
            'Пикантная пепперони, увеличенная порция моцареллы, томатный соус',
        },
        {
          id: 4,
          title: 'Большой Стен',
          price: 450,
          img:
            'https://dodopizza-a.akamaihd.net/static/Img/Products/Pizza/ru-RU/dc5dc4e9-932a-4abf-9472-dfb6326ea9ee.jpg',
          description:
            'Пикантная пепперони, увеличенная порция моцареллы, томатный соус',
        },
      ],
    }
  },
  mounted() {},
  methods: {},
}
</script>
<style scoped>
.recommended--list {
  overflow-x: auto;
  /* flex-wrap: wrap; */
  margin-top: 10px;
}
.recommended--item {
  border-radius: 20px;
  /* width: 350px; */
  padding: 20px;
  display: flex;
  justify-content: center;
}
.recommended--item div {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  font-size: 20px;
  margin-left: 15px;
}
/* полоса прокрутки (скроллбар) */
::-webkit-scrollbar {
  width: 24px; /* ширина для вертикального скролла */
  height: 8px; /* высота для горизонтального скролла */
  background-color: #fff;
}

/* ползунок скроллбара */
::-webkit-scrollbar-thumb {
  background-color: #ffd000;
  border-radius: 9em;
  box-shadow: inset 1px 1px 10px #f3faf7;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #c8ff00;
}

/* Стрелки */

::-webkit-scrollbar-button:vertical:start:decrement {
  background: linear-gradient(120deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(240deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(0deg, #02141a 30%, rgba(0, 0, 0, 0) 31%);
  background-color: #f6f8f4;
}

::-webkit-scrollbar-button:vertical:end:increment {
  background: linear-gradient(300deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(60deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(180deg, #02141a 30%, rgba(0, 0, 0, 0) 31%);
  background-color: #f6f8f4;
}

::-webkit-scrollbar-button:horizontal:start:decrement {
  background: linear-gradient(30deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(150deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(270deg, #02141a 30%, rgba(0, 0, 0, 0) 31%);
  background-color: #f6f8f4;
}

::-webkit-scrollbar-button:horizontal:end:increment {
  background: linear-gradient(210deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(330deg, #02141a 40%, rgba(0, 0, 0, 0) 41%),
    linear-gradient(90deg, #02141a 30%, rgba(0, 0, 0, 0) 31%);
  background-color: #f6f8f4;
}
</style>

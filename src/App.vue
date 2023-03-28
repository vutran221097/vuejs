<template>
  <h1>Giỏ hàng</h1>
  <h3>{{ shirtItem.title }}</h3>
  <div class="shirt-item">
    <div :style="{ marginRight: 20 + 'px' }">
      <img :src="require(`@/assets/${shirtPickedItem.url}`)" width="400" height="500">
    </div>

    <div>
      <h2 v-if="shirtPickedItem.stock">Còn lại: {{ shirtPickedItem.stock }} sản phẩm</h2>
      <h2 v-if="!shirtPickedItem.stock">Sản phẩm hết hàng</h2>

      <h2>Giá: {{ formatFinalPrice }}</h2>

      <div class="original-price">
        <h3 :style="{ color: 'grey', textDecoration: 'line-through' }">{{ formatOriginalPrice }}
        </h3>
        <div class="sale-percentage">
          {{ formatSaleNumber }}
        </div>
      </div>

      <div class="list-item-color">
        <div v-for="(item, index) in shirtItem.color" :key="index" class='item' v-on:click="changeShirtColor(item.name)">
          <img :src="require(`@/assets/${item.url}`)" width="50" height="50">
        </div>
      </div>

      <div v-for="(item, index) in description" :key="index" class="description">
        <li>{{ item }}</li>
      </div>

    </div>

  </div>
</template>

<script>
// import ToDoList from './components/ToDoList.vue'

export default {
  name: 'App',
  // components: {
  //   ToDoList
  // }
  data() {
    return {
      shirtPicked: "white",
      shirtItem: {
        title: "Áo Phông - Simon - Slim Fit",
        price: 50000,
        sale: 0.5,
        color: [{
          name: "white",
          url: "white-shirt.jpg",
          stock: 8
        }, {
          name: "brown",
          url: "brown-shirt.jpg",
          stock: 5
        }, {
          name: "darkGreen",
          url: "dark-green-shirt.jpg",
          stock: 0
        }]
      },
      description: [
        "Chất liệu: thun", "Thoát mồ hôi tốt", "Áo phông Simon thời trang sành điệu"
      ]
    }
  },
  methods: {
    changeShirtColor(color) {
      return this.shirtPicked = color
    }
  },
  computed: {
    shirtPickedItem: function () {
      return this.shirtItem.color.find(item => item.name === this.shirtPicked)
    },
    shirtPrice: function () {
      return this.shirtItem.price * this.shirtItem.sale
    },
    formatOriginalPrice: function () {
      return this.shirtItem.price.toLocaleString('it-IT', { style: 'currency', currency: 'VND' });
    },
    formatFinalPrice: function () {
      const finalPrice = this.shirtItem.price * this.shirtItem.sale
      return finalPrice.toLocaleString('it-IT', { style: 'currency', currency: 'VND' });
    },
    formatSaleNumber: function () {
      return '-' + this.shirtItem.sale * 100 + "%"
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.shirt-item {
  display: flex;
  justify-content: center;
}

.sale-percentage {
  border: 2px solid black;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 10px;
  margin-top: 5px;
  padding: 5px;
  height: 30px;
  width: 30px;
}

.original-price {
  display: flex;
  justify-content: center;
}

.description {
  display: flex;
  justify-content: start;
}

.list-item-color {
  display: flex;
  justify-content: start;
  margin-bottom: 10px;
  height: 50px;
}

.item {
  margin-right: 10px;
}

.item img:hover {
  border: 2px solid blue;
}
</style>

<script setup lang="ts">
import {ref, reactive, watch, toRefs } from 'vue';

const itemName2 = "Bike"

const item1 = reactive({
  name: "Deck",
  price: 40000
})

const price2 = 20000

const url1 = "https://gaming.logicool.co.jp/ja-jp/logitech-g-and-herman-miller.html"

const buy = (itemName: string) => {
  alert("Are you sure to buy " + itemName + "?");
}

const clear = () => {
  item1.name = ''
  item1.price = 0
}

const budget = 50000

const priceLabel = ref<string>(`${item1.price} yen`)
const { price } = toRefs(item1)
watch(price, () => {
console.log("watch")
if (price.value > budget * 2) {
  priceLabel.value = "tooooo expensive..."
} else if (price.value > budget) {
  priceLabel.value = "expensive..."
} else {
  priceLabel.value = `${price.value} yen`
}
})

</script>

<template>
  <div class="container">
    <h1>payment</h1>
    <h2 class="input-form">inputName</h2>
    <input class="input" v-model="item1.name" />
    <h2 class="input-form">inputPrice</h2>
    <input class="input" v-model="item1.price" />
    <button class="clear" v-on:click="clear">Clear</button>
    <div class="payment">
      <label>{{ item1.name }}</label>
      <label>{{ priceLabel }}</label>
      <a v-bind:href="url1">bought at...</a>
      <button v-on:click="buy(item1.name)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ itemName2 }}</label>
      <label>{{ price2 }} yen</label>
      <button v-on:click="buy(itemName2)">BUY</button>
    </div>
  </div>
</template>

<style scoped>
.input-form {
  margin: 5px 0;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.input {
  height: 40px;
  width: 300px;
  margin-bottom: 20px;
}
.clear {
  margin-bottom: 10px;
}
.payment {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 80px;
  width: 400px;
  background-color: #646cffaa;
  margin-bottom: 8px;
  padding: 8px;
  border-radius: 8px;
}
label {
  font-size: 20px;
  font-weight: bold;
}
</style>

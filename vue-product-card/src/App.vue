
<template>
  <div id="app">
    <div class="product">
      <div class="product-image">
        <img v-bind:src="image" v-bind:alt="altText" />
      </div>

      <div class="product-info">
        <h1>{{ product }}</h1>
        <!--        <p>{{ description }}</p> -->
        <!--        <a :href="link" target="_blank">More products like this</a> -->
        <p v-if="inventory > 10">In stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost Sold Out</p>
        <p v-else>Out of stock</p>
        <span v-show="onSale">On Sale</span>
        <ul>
          <li v-for="(detail, index) of details" :key="index">{{ detail }}</li>
        </ul>
        <div
          class="color-box"
          v-for="variant of variants"
          :key="variant.variantId"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(variant.variantImage)"
        ></div>
        <ul>
          <li v-for="(size, index) of sizes" :key="index">{{ size }}</li>
        </ul>
        <div class="cart">
          <p>Cart ({{ cart }})</p>
        </div>
        <button
          v-on:click="addToCart"
          :disabled="!inStock"
          :class="{ disabledButton: !inStock }"
        >
          Add to cart
        </button>
        <button @click="removeFromCart">remove from cart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: "Socks",
      // description: 'A pair of warm, fuzzy socks',
      image:
        "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
      altText: "A pair of socks",
      // link: "https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks",
      inStock: true,
      inventory: 100,
      onSale: true,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImage:
            "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
        },
      ],
      sizes: ["S", "M", "L", "XL", "XXL", "XXXL"],
      cart: 0,
    };
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
    updateProduct(variantImage) {
      this.image = variantImage;
    },
    removeFromCart() {
      if (this.cart > 0) {
        this.cart -= 1;
      } else return this.cart;
    },
  },
};
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
}

.product-info {
  margin-top: 10px;
  flex-basis: 500px;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1E95EA;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
} 

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 30%;
  padding: 20px;
  border: 1px solid #d8d8d8;  
}

input {
  width: 100%;  
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}
</style>

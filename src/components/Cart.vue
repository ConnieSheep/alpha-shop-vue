<template>
  <div class="cart-panel">
    <h2 class="shopping-cart">購物籃</h2>
    <div v-for="product in products" :key="product.id" class="product">
      <img :src="product.image" alt="" />
      <div class="product-description">
        <div class="product-control">
          <div>{{ product.name }}</div>
          <div class="amount-control">
            <span @click.stop.prevent="minusQuantity(product.id)" class="minus">
              －</span
            >
            <span class="number">{{ product.quantity }}</span>
            <span @click.stop.prevent="plusQuantity(product.id)" class="plus"
              >＋
            </span>
          </div>
        </div>
        <div class="product-price">
          <span>$</span>
          <span>{{ product.price * product.quantity | addComma }}</span>
        </div>
      </div>
    </div>
    <div class="fee">
      <div>運費</div>
      <div>{{ deliveryFee ? '$500' : '免費' }}</div>
    </div>
    <div class="fee">
      <div>小計</div>
      <div>
        <span>$</span>
        <span>{{ totalPrice | addComma }}</span>
      </div>
    </div>
  </div>
</template>

<script>
const dummyData = {
  products: [
    {
      id: 1,
      name: '破壞補釘修身牛仔褲',
      image: 'https://i.postimg.cc/BZ5YL2Bf/Block-2px.png',
      price: 3999,
      quantity: 1
    },
    {
      id: 2,
      name: '刷色直筒牛仔褲',
      image: 'https://i.postimg.cc/dQz8NvZJ/Block-2x.png',
      price: 1299,
      quantity: 1
    }
  ]
}

export default {
  props: {
    deliveryFee: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      products: []
    }
  },
  created() {
    this.fetchProducts()
  },
  methods: {
    fetchProducts() {
      this.products = dummyData.products
    },
    plusQuantity(productId) {
      this.products = this.products.map((product) => {
        if (product.id === productId) {
          return {
            ...product,
            quantity: product.quantity + 1
          }
        }
        return product
      })
    },
    minusQuantity(productId) {
      this.products = this.products.map((product) => {
        if (product.id === productId && product.quantity > 0) {
          return {
            ...product,
            quantity: product.quantity - 1
          }
        }
        return product
      })
    }
  },
  computed: {
    totalPrice() {
      let productPrice = 0
      this.products.forEach((product) => {
        return (productPrice += product.price * product.quantity)
      })
      if (this.deliveryFee) {
        return productPrice + 500
      }
      return productPrice
    }
  },
  filters: {
    addComma(price) {
      return price.toLocaleString()
    }
  }
}
</script>

<style scoped>
.cart-panel {
  height: 95%;
  border: 1px solid lightgray;
  padding: 30px;
  border-radius: 10px;
  margin: 70px 0 30px 0;
}
.shopping-cart {
  height: 8%;
}
.product {
  height: 20%;
  margin-top: 40px;
  display: flex;
}
.product-description {
  width: 100%;
  display: flex;
  justify-content: space-between;
  margin-left: 15px;
  line-height: 30px;
}
img {
  height: 100px;
  width: 100px;
}
.minus,
.plus {
  height: 24px;
  width: 24px;
  color: white;
  border-radius: 50%;
  background-color: lightgray;
  cursor: pointer;
}
.number {
  margin: 0 20px;
}
.product-price {
  font-weight: 700;
}
.fee {
  font-weight: 700;
  display: flex;
  justify-content: space-between;
  border-top: 1px solid lightgray;
  margin-top: 50px;
  padding-top: 50px;
}
</style>
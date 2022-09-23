<template>
  <div class="container">
    <div class="user-info">
      <Step :step="step" />
      <Form
        :step="step"
        :initial-fee="deliveryFee"
        @handleFee="setDeliveryFee"
      />
      <div class="btn-panel">
        <button
          v-if="step > 1"
          @click.stop.prevent="previousStep"
          class="previous-step"
        >
          ← 上一步
        </button>
        <button v-else disabled></button>
        <button @click.stop.prevent="nextStep" class="next-step">
          {{ step === 3 ? '送出訂單' : '下一步 →' }}
        </button>
      </div>
    </div>
    <div class="cart-info">
      <Cart :delivery-fee="deliveryFee" />
    </div>
  </div>
</template>

<script>
import Step from '../components/Step'
import Form from '../components/Form'
import Cart from '../components/Cart'

export default {
  data() {
    return {
      step: 1,
      deliveryFee: false
    }
  },
  components: {
    Step,
    Form,
    Cart
  },
  methods: {
    previousStep() {
      if (this.step > 1) {
        this.step = this.step - 1
      }
    },
    nextStep() {
      if (this.step < 3) {
        this.step = this.step + 1
      }
    },
    setDeliveryFee(e) {
      this.deliveryFee = e
    }
  }
}
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  height: 100vh;
  width: 90%;
  margin: auto;
}
.user-info {
  height: 80vh;
  margin: auto;
  width: 50%;
  margin-right: 5%;
}
.cart-info {
  height: 80vh;
  margin: auto;
  width: 50%;
  margin-left: 5%;
}
.btn-panel {
  height: 10%;
  display: flex;
  justify-content: space-between;
  margin-top: 50px;
  border-top: 1px solid lightgray;
  padding-top: 40px;
}
.previous-step,
.next-step {
  height: 46px;
  width: 174px;
  font-size: 16px;
  border: none;
  cursor: pointer;
  border-radius: 8px;
}
.previous-step {
  background: white;
}
.next-step {
  background: #f67599;
  color: white;
}
</style>
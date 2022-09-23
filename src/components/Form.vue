<template>
  <div class="form-panel">
    <form action="">
      <div v-show="step === 1" class="delivery-address">
        <div class="form-title">
          <h2>寄送地址</h2>
        </div>
        <div class="title">
          <label for="">稱謂</label>
          <div class="select-wrapper">
            <select name="" id="">
              <option value="" disabled selected>請選擇稱謂</option>
              <option value="male">先生</option>
              <option value="female">小姐</option>
            </select>
          </div>
        </div>
        <div class="name">
          <label for="">姓名</label>
          <input type="text" placeholder="請輸入姓名" />
        </div>
        <div class="phone">
          <label for="">電話</label>
          <input type="text" placeholder="請輸入電話" />
        </div>
        <div class="email">
          <label for="">Email</label>
          <input type="text" placeholder="請輸入電子郵件" />
        </div>
        <div class="city">
          <label for="">縣市</label>
          <div class="select-wrapper">
            <select name="" id="">
              <option value="" disabled selected>請選擇縣市</option>
              <option value="">臺北市</option>
              <option value="">新北市</option>
              <option value="">桃園市</option>
            </select>
          </div>
        </div>
        <div class="address">
          <label for="">地址</label>
          <input type="text" placeholder="請輸入地址" />
        </div>
      </div>
      <div v-show="step === 2" class="delivery-type">
        <div class="form-title">
          <h2>運送方式</h2>
        </div>
        <div class="standard">
          <div class="radio-container" :class="{ active: fee === false }">
            <input
              type="radio"
              name="delivery"
              checked
              @click="free"
              @change="handleFee"
            />
            <label for="">
              <div class="type-name">
                <div>標準運送</div>
                <div>免費</div>
              </div>
              <div class="standard-time">約 3 ~ 7 個工作天</div>
            </label>
          </div>
        </div>
        <div class="DHL">
          <div class="radio-container" :class="{ active: fee === true }">
            <input
              type="radio"
              name="delivery"
              @click="addFee"
              @change="handleFee"
            />
            <label for="">
              <div class="type-name">
                <div>DHL 貨運</div>
                <div>$500</div>
              </div>
              <div class="DHL-time">48 小時內送達</div>
            </label>
          </div>
        </div>
      </div>
      <div v-show="step === 3" class="payment-info">
        <div class="form-title">
          <h2>付款資訊</h2>
        </div>
        <div class="card-name">
          <label for="">持卡人姓名</label>
          <input type="text" placeholder="John Doe" />
        </div>
        <div class="card-number">
          <label for="">卡號</label>
          <input type="text" placeholder="1111 2222 3333 4444" />
        </div>
        <div class="card-valid">
          <label for="">有效期限</label>
          <input type="text" placeholder="MM/YY" />
        </div>
        <div class="card-code">
          <label for="">CVC/CCV</label>
          <input type="text" placeholder="123" />
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    step: {
      type: Number,
      required: true
    },
    deliveryFee: {
      type: Boolean,
      require: true
    }
  },
  data() {
    return {
      fee: this.deliveryFee
    }
  },
  methods: {
    addFee() {
      this.fee = true
    },
    free() {
      this.fee = false
    },
    handleFee() {
      const shippingFee = this.fee
      this.$emit('handleFee', shippingFee)
    }
  }
}
</script>

<style scoped>
.form-panel {
  height: 60%;
}
.delivery-address {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: 60px 1fr 1fr 1fr;
  gap: 25px;
}
.delivery-address .form-title {
  grid-column: 1 / 3;
}
.title {
  grid-column: 1 / 3;
  grid-row: 2;
}
.name {
  grid-column: 3 / 7;
  grid-row: 2;
}
.phone {
  grid-column: 1 / 4;
  grid-row: 3;
}
.email {
  grid-column: 4 / 7;
  grid-row: 3;
}
.city {
  grid-column: 1 / 3;
  grid-row: 4;
}

.address {
  grid-column: 3 / 7;
  grid-row: 4;
}
.delivery-type {
  display: grid;
}
.payment-info {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: 60px 1fr 1fr 1fr;
  gap: 25px;
}
.payment-info .form-title {
  grid-column: 1 / 2;
}
.card-name {
  grid-column: 1 / 3;
  grid-row: 2;
}
.card-number {
  grid-column: 1 / 3;
  grid-row: 3;
}
.card-valid {
  grid-column: 1 / 2;
  grid-row: 4;
}
.card-code {
  grid-column: 2 / 3;
  grid-row: 4;
}
.select-wrapper {
  position: relative;
  width: 100%;
  z-index: 0;
}
.select-wrapper::after {
  content: '';
  border-style: solid;
  border-width: 6px 5px 0 5px;
  border-color: black transparent transparent transparent;
  position: absolute;
  top: 50%;
  right: 8px;
  transform: translateY(-50%);
  z-index: -1;
}
label {
  display: block;
  margin-bottom: 6px;
  font-weight: 500;
}
input,
select,
.radio-container {
  height: 50px;
  width: 100%;
  color: black;
  border: 1px solid lightgray;
  border-radius: 5px;
  font-size: 16px;
  padding: 0.5em;
  margin-bottom: 6px;
}
input:hover,
input:focus,
select:hover,
select:focus {
  border-color: black;
}

input[type='radio'] {
  -webkit-appearance: none;
  border-radius: 50%;
  cursor: pointer;
  height: 24px;
  width: 24px;
  margin-top: 10px;
  margin-right: 15px;
}
input[type='radio']:checked {
  box-shadow: inset 0 0 0 5px black;
}
.radio-container {
  margin-top: 30px;
  height: 85%;
  display: flex;
  align-items: center;
  padding-right: 15px;
}
.radio-container label {
  width: 100%;
}
.type-name {
  display: flex;
  justify-content: space-between;
}
.standard {
  margin: 30px 0 10px 0;
}
.active {
  border: 1px solid black;
}
</style>
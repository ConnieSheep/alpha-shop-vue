<template>
  <div class="stepper-panel">
    <h2>結帳</h2>
    <div class="stepper-container">
      <div class="step active" :class="{ checked: step > 1 }">
        <div class="circle-container one"></div>
        <div class="label-container">寄送地址</div>
      </div>
      <div class="step" :class="{ checked: step === 3, active: step === 2 }">
        <div class="circle-container two"></div>
        <span class="connect-line"></span>
        <div class="label-container">運送方式</div>
      </div>
      <div class="step" :class="{ active: step === 3 }">
        <div class="circle-container three"></div>
        <span class="connect-line"></span>
        <div class="label-container">付款資訊</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    step: {
      type: Number,
      required: true
    }
  }
}
</script>

<style scoped>
.stepper-panel {
  height: 20%;
}
.stepper-container {
  display: flex;
  margin-top: 40px;
}
.step {
  display: flex;
  justify-content: center;
  flex: 1;
  text-align: center;
  position: relative;
}
.circle-container {
  height: 24px;
  width: 24px;
  padding-top: 3px;
  color: lightgray;
  border-radius: 50%;
  border: 1px solid lightgray;
}
.connect-line {
  display: block;
  height: 1px;
  background: lightgray;
  position: absolute;
  top: 12px;
  right: calc(40% + 90px);
  left: calc(-40% + 40px);
}
.label-container {
  margin-left: 5px;
  color: lightgray;
}
.one::after {
  content: '1';
}
.two::after {
  content: '2';
}
.three::after {
  content: '3';
}
.checked .circle-container::after {
  content: '\2714';
}
.checked .circle-container,
.active .circle-container {
  color: white;
  background: black;
}
.checked .connect-line,
.active .connect-line {
  height: 2px;
  background: black;
}
.checked .label-container,
.active .label-container {
  color: black;
}
</style>
<template>
  <div class="calculator">
    <div class="main-display">
      <div class="total">{{ total }}</div>
      <div class="number-input">{{ displayVal }}</div>
    </div>

    <div class="btns-wrapper">
      <button class="btn" @click="clear">C</button>

      <button class="btn" @click="count('/')">/</button>
      <button class="btn" @click="count('*')">*</button>
      <button class="btn" @click="count('-')">-</button>
      <button class="btn" @click="count('+')">+</button>

      <button class="btn solve" @click="solve">=</button>

      <div class="nums">
        <button class="btn" v-for="num in 3" :key="num+6" @click="setNum(`${num +6}`)">{{ num+6 }}</button>
        <button class="btn" v-for="num in 3" :key="num+3" @click="setNum(`${num +3}`)">{{ num+3 }}</button>
        <button class="btn" v-for="num in 3" :key="num" @click="setNum(`${num}`)">{{ num }}</button>

        <button class="btn" @click="setNum('00')">00</button>
        <button class="btn" @click="setNum('0')">0</button>
        <button class="btn" @click="setNum('.')">,</button>
      </div>


    </div>
  </div>
</template>

<script>
export default {
  name: "SimpleCalculator",
  data() {
    return {
      displayVal: '',
      total: '',
      operator: '',
      num: '',

    }
  },
  created() {
    document.title = 'Calculator Vue.js 3'
  },
  methods: {
    setNum(str) {
      if (this.operator == '' && this.num == '' && this.total == '') {
        this.displayVal = str
        this.num = str
      }
      else {
        this.displayVal += str
        this.num += str

      }
    },
    count(newOperator) {
      this.displayVal += ` ${newOperator} `
      if (this.total == '' ) {
        this.total = parseFloat(this.num)
        this.displayVal = this.total + ` ${newOperator} `
      } else if (this.operator == '+') {
        this.total += parseFloat(this.num)
      } else if (this.operator == '-') {
        this.total -= parseFloat(this.num)
      } else if (this.operator == '*') {
        this.total = this.total * parseFloat(this.num)
      } else if (this.operator == '/') {
        this.total = this.total / parseFloat(this.num)
      }
      this.operator = newOperator
      this.num = ''
    },
    solve() {
      this.count('')
    },
    clear() {
      this.total = ''
      this.num = ''
      this.operator = ''
      this.displayVal = ''
    },

  },
}
</script>

<style lang="scss">
.calculator {
  width: 500px;
  border: solid 1px #eee;
  margin: 0 auto;
  background-color: rgb(42, 30, 59, .8);
  display: grid;
  box-sizing: border-box;
  border-radius: 4px;

  .main-display {
    display: grid;
    background-color: rgba(19, 5, 38, 0.8);
    border: 1px solid rgba(255, 255, 255, .8);
    box-shadow: rgba(255, 255, 255, .8) 4px 4px 0 0, rgba(0, 0, 0, 0.79) 4px 4px 0 1px;
    border-radius: 4px;
    margin: 1em;
    cursor: text;

    .total {
      height: 100px;
      color: #fff;
      font-size: 40px;
      justify-self: end;
      display: grid;
      align-items: end;
      margin-right: 5px;
      margin-bottom: 5px;
    }

    .number-input {
      height: 100px;
      color: rgba(255, 255, 255, 0.56);
      font-size: 24px;
      justify-self: end;
      display: grid;
      align-items: end;
      margin-right: 5px;
      margin-bottom: 5px;
    }
  }

  .btns-wrapper {
    display: grid;
    margin: 1em;
    grid-template-columns: repeat(4, 1fr);

    .nums {
      grid-column-start: 1;
      grid-column-end: 4;
      grid-row-start: 2;
      grid-row-end: 4;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
    }

    .btn {
      min-height: 80px;
      background-color: rgba(19, 5, 38, 0.8);
      border: 1px solid #000;
      border-radius: 4px;
      box-shadow: rgba(255, 255, 255, .8) 4px 4px 0 0, rgba(0, 0, 0, 0.79) 4px 4px 0 1px;
      color: #fff;
      cursor: pointer;
      display: inline-block;
      font-size: 24px;
      font-weight: 400;
      margin: 0 5px 10px 0;
      padding: 1em;
      text-align: center;
      touch-action: manipulation;
      user-select: none;

      &:focus {
        text-decoration: none;
      }

      &:hover {
        background-color: rgba(44, 14, 84, 0.8);
      }

      &:active {
        box-shadow: rgba(0, 0, 0, .125) 0 3px 5px inset;
        outline: 0;
      }

      &:not([disabled]):active {
        box-shadow: rgba(255, 255, 255, .8) 2px 2px 0 0, rgba(0, 0, 0, 0.79) 2px 2px 0 1px;
        transform: translate(2px, 2px);
      }
    }

  }

}


</style>
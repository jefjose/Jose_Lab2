<template>
  <div class="calculator">
    <input class="display" type="text" v-model="display" readonly>
    <div class="button-row">
      <button class="button" @click="clearDisplay">C</button>
      <button class="button operator" @click="appendToDisplay('/')">/</button>
      <button class="button operator" @click="appendToDisplay('*')">*</button>
      <button class="button" @click="deleteLastCharacter">DEL</button>
    </div>
    <div class="button-row">
      <button class="button" @click="appendToDisplay('7')">7</button>
      <button class="button" @click="appendToDisplay('8')">8</button>
      <button class="button" @click="appendToDisplay('9')">9</button>
      <button class="button operator" @click="appendToDisplay('-')">-</button>
    </div>
    <div class="button-row">
      <button class="button" @click="appendToDisplay('4')">4</button>
      <button class="button" @click="appendToDisplay('5')">5</button>
      <button class="button" @click="appendToDisplay('6')">6</button>
      <button class="button operator" @click="appendToDisplay('+')">+</button>
    </div>
    <div class="button-row">
      <button class="button" @click="appendToDisplay('1')">1</button>
      <button class="button" @click="appendToDisplay('2')">2</button>
      <button class="button" @click="appendToDisplay('3')">3</button>
      <button class="button equal" @click="calculate">=</button>
    </div>
    <div class="button-row">
      <button class="button" @click="appendToDisplay('%')">%</button>
      <button class="button" @click="appendToDisplay('0')">0</button>
      <button class="button" @click="appendToDisplay('.')">.</button>
      <button class="button-jose" readonly></button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: ''
    };
  },
  methods: {
    appendToDisplay(char) {
      if (this.display === 'Error') {
        this.display = '';
      }
      if (char === '%') {
        this.display += '/100';
      } else {
        this.display += char;
      }
    },
    clearDisplay() {
      this.display = '';
    },
    deleteLastCharacter() {
      this.display = this.display.slice(0, -1);
    },
    calculate() {
      if (this.display !== 'Error') {
        try {
          this.display = eval(this.display).toString();
        } catch (error) {
          this.display = 'Error';
        }
      }
    }
  }
};
</script>

<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .calculator {
    width: 300px;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
    background-color: #eaeaea;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%); 
  }
  .display {
    width: calc(100% + 10px);
    height: 60px;
    margin: 0 5px 10px;
    padding: 10px;
    border: none;
    border-radius: 5px;
    background-color: #fff;
    font-size: 24px;
    text-align: right;
  }
  .button-row {
    display: flex;
    justify-content: center;
  }
  .button {
    width: 60px;
    height: 60px;
    margin: 5px;
    border: none;
    border-radius: 50%; 
    cursor: pointer;
    font-size: 20px;
    background-color: #ddd;
    transition: background-color 0.3s;
  }
  .button-jose {
    width: 60px;
    height: 60px;
    margin: 5px;
    border: none;
    border-radius: 50%;
    cursor: default;
    font-size: 20px;
    background-color: #ddd;
  }
  .button:hover {
    background-color: #ccc;
  }
  .button.operator {
    background-color: #f0ad4e;
    color: #fff;
  }
  .button.equal {
    background-color: #5cb85c;
    color: #fff;
  }
</style>

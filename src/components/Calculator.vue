<template>
  <div class="calculator">
    <div class="display">{{number}}</div>
    <div class="box" @click="append('9')">9</div>
    <div class="box" @click="append('8')">8</div>
    <div class="box" @click="append('7')">7</div>
    <div class="box operator" @click="operation('/')">/</div>
    <div class="box" @click="append('6')">6</div>
    <div class="box" @click="append('5')">5</div>
    <div class="box" @click="append('4')">4</div>
    <div class="box operator" @click="operation('*')">*</div>
    <div class="box" @click="append('3')">3</div>
    <div class="box" @click="append('2')">2</div>
    <div class="box" @click="append('1')">1</div>
    <div class="box operator" @click="operation('-')">-</div>
    <div class="box" @click="operation('%')">%</div>
    <div class="box" @click="negate">+/-</div>
    <div class="box" @click="dot">.</div>
    <div class="box operator" @click="operation('+')">+</div>
    <div class="box xero" @click="append('0')">0</div>
    <div class="box" @click="ans">=</div>
    <div class="box clear" @click="reset">AC</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      number: "",
      previous: null,
      calc: null
    };
  },
  methods: {
    reset: function() {
      this.number = "";
    },
    append: function(num) {
      this.number += num;
    },
    operation: function(operation) {
      this.previous = this.number;
      this.number = "";
      if (operation === "+") {
        this.calc = (a, b) => a + b;
      }
      if (operation === "-") {
        this.calc = (a, b) => a - b;
      }
      if (operation === "*") {
        this.calc = (a, b) => a * b;
      }
      if (operation === "/") {
        this.calc = (a, b) => b / a;
      }
      if (operation === "%") {
        this.calc = (a, b) => b % a;
      }
    },
    dot: function() {
      if (this.number.indexOf(".") == -1) {
        this.append(".");
      }
    },
    ans: function() {
      this.number = this.calc(
        parseFloat(this.number),
        parseFloat(this.previous)
      );
    },
    negate: function() {
      this.number = this.number + "";
      if (this.number.charAt(0) == "-") {
        this.number = this.number.slice(1);
      } else {
        this.number = "-" + this.number;
      }
    }
  }
};
</script>

<style scoped>
.calculator {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 320px;
  padding: 30px 20px;
  background: rgba(3, 37, 53, 0.6);
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: minmax(50px, auto);
  grid-auto-rows: 50px;
  grid-gap: 2px;
  font-size: 20px;
  cursor: pointer;
}

.box {
  /* background: lightgray; */
  /* background: lightgray; */
  color: white;
  border: 1px solid rgba(1, 1, 1, 0.3);
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}

.box:hover {
  background: gray;
}

.operator {
  background: orange;
}

.clear {
  border: 1px solid rgba(1, 1, 1, 0.1);
  text-align: center;
  background: black;
  color: white;
  grid-column: 4/5;
}

.clear:hover {
  background: gray;
}

.xero {
  grid-column: 1/3;
}

.display {
  grid-column: 1 / 5;
  background: #cccbcb;
  border-radius: 2px;
  display: flex;
  justify-content: flex-end;
  align-items: flex-end;
  padding: 5px;
}
</style>
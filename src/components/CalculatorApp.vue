<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="plusMinus" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">/</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: "CalculatorApp",
  data() {
    return {
      current: "",
      previous: "",
      operator: null,
      operatorClicked: false,
    };
  },

  methods: {
    clear() {
      this.current = "";
    },
    plusMinus() {
      this.current = this.current * -1;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        (this.current = ""), (this.operatorClicked = false);
      }
      this.current = this.current + number;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      );
      this.previous = null;
    },
  },
};
</script>

<style scoped>
.calculator {
  font-size: 40px;
  max-width: 350px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  border: 4px solid #001825;
  border-top: none;
  border-radius: 3px;
  margin-top: 5%;
  user-select: none;
}
.calculator div {
  height: 70px;
}

.display {
  grid-column: 1 /5;
  background-color: #001825;
  color: rgb(233, 233, 233);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 45px;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #f2f2f2;
  border: 1px solid #001825;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.1s;
}

.btn:hover {
  background-color: #001825;
  color: white;
}

.operator {
  background-color: #f4a261;
  color: white;
}

.operator:hover {
  background-color: #e76f51;
  color: white;
}

@media (max-width: 400px) {
  .calculator {
    max-width: 300px;
    max-height: 500px;
    font-size: 35px;
  }
}
</style>

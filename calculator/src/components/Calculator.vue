<template>
  <div class="calculator">
    <ul>
      <li class="display">{{ current || 0 }}</li>
      <li @click="clear()" class="btn">C</li>
      <li @click="sign()" class="btn">+/-</li>
      <li @click="percent()" class="btn">%</li>
      <li @click="divide()" class="btn operator">/</li>
      <li @click="append('7')" class="btn">7</li>
      <li @click="append('8')" class="btn">8</li>
      <li  @click="append('9')" class="btn">9</li>
      <li @click="times()" class="btn operator">x</li>
      <li @click="append('4')" class="btn">4</li>
      <li @click="append('5')" class="btn">5</li>
      <li @click="append('6')" class="btn">6</li>
      <li @click="minus()" class="btn operator">-</li>
      <li @click="append('1')" class="btn">1</li>
      <li @click="append('2')" class="btn">2</li>
      <li @click="append('3')" class="btn">3</li>
      <li @click="add()" class="btn operator">+</li>
      <li @click="append('0')" class="btn zero">0</li>
      <li @click="dot()" class="btn">.</li>
      <li @click="equal()" class="btn operator">=</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data(){
    return {
      current: '12',
      previous: null,
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
          this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
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
    times() {
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
      this.current = `${this.operator(
          parseFloat(this.current),
          parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator{
  padding: 20px;
}
.display {
  grid-column: 1 / 5;
  background-color: #202020;
  color: white;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding: 10px;
}

ul {
  width: 300px;
  margin: 0 auto;
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  text-align: center;
}

ul li {
  list-style: none;
  cursor: pointer;
}


.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #D4D6D8;
  border: 1px solid #5B5B5C;
}

.btn:hover{
  background-color: #b1b2b3;
}
.operator {
  background-color: #F98E10;
  color: white;
}

.operator:hover{
  background-color: #F98E10;
}
</style>

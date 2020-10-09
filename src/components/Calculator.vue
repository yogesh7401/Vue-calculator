<template>
  <div>
    <h1>Calculator</h1>
    <div class='calculator' onselectstart='return false'>
      <div class='display'>{{display}}</div>                        <!-- Display -->
      <div @click='erase' class='button darker'>C</div>             <!-- Clear the Display -->
      <div @click='opp' class='button darker'>+/-</div>             <!-- Select operation -->
      <div @click='percent' class='button darker'>%</div>           <!-- Give percentage value -->
      <div @click='divide' class='button operator'>÷</div>          <!-- Divide operation -->
      <div @click='append(1)' class='button'>1</div>                <!-- Append 1 in display -->
      <div @click='append(2)' class='button'>2</div>                <!-- Append 2 in display -->
      <div @click='append(3)' class='button'>3</div>                <!-- Append 3 in display -->
      <div @click='product' class='button operator'>x</div>         <!-- Product operation -->
      <div @click='append(4)' class='button'>4</div>                <!-- Append 4 in display -->
      <div @click='append(5)' class='button'>5</div>                <!-- Append 5 in display -->
      <div @click='append(6)' class='button'>6</div>                <!-- Append 6 in display -->
      <div @click='sub' class='button operator'>-</div>             <!-- Subraction operation -->
      <div @click='append(7)' class='button'>7</div>                <!-- Append 7 in display -->
      <div @click='append(8)' class='button'>8</div>                <!-- Append 8 in display -->
      <div @click='append(9)' class='button'>9</div>                <!-- Append 9 in display -->
      <div @click='add' class='button operator'>+</div>             <!-- Add operation -->
      <div @click='append(0)' class='button zero button-bottom'>0</div>    <!-- Append 0 in display -->
      <div @click='decimal' class='button darker button-bottom'>.</div>    <!-- Append decimal in display -->
      <div @click='equal' class='button operator button-bottom'>=</div>    <!-- Equal Operator -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      display: 0,
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    erase() {
      this.display = 0;
    },
    opp() {
      this.display =
        this.display < 0 ? (this.display = this.display - this.display * 2) : (this.display = this.display - this.display * 2);
    },
    percent() {
      this.display = this.display / 100;
    },
    append(number) {
      if (this.operatorClicked === true) {
        this.display = '';
        this.operatorClicked = false;
      }
      this.display =
        this.display === 0
          ? (this.display = number)
          : '' + this.display + number;
    },
    decimal() {
      if (this.display.indexOf('.') === -1) {
        this.append('.');
      }
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    product() {
      this.operator = (a, b) => a * b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    sub() {
      this.operator = (a, b) => a - b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    add() {
      this.operator = (a, b) => a + b;
      this.previous = this.display;
      this.operatorClicked = true;
    },
    equal() {
      this.display = this.operator(Number(this.previous), Number(this.display));
      this.previous = null;
      this.operatorClicked = true;
    }
  }
};
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 80vw;
  font-size: 2rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  border: 5px solid #111;
  box-shadow: -3px 3px 15px rgba(17,17,17,0.4);
  line-height: 10vh;
}

.display {
  grid-column: 1 / 5;
  background: #f7e5e5;
  border: 1px solid #111;
  font-size: 2.5rem;
  cursor: default;
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 1rem;
}

.button {
  background: linear-gradient(15deg,hsl(0, 6%, 68%) 0%, hsl(0, 0%, 80%) 100%);
  border: 1px solid #111;
  cursor: pointer;
}

.button:active {
  outline:none;
  border: 1px solid #000000BF; 
  box-shadow: inset 0px 0px 5px #00000080; 
  -moz-box-shadow: inset 0px 0px 5px #00000080;
  -webkit-box-shadow: inset 0px 0px 5px #00000080;
}

.zero {
  grid-column: 1 / 3;
}

.operator {
  background: hsl(39, 88%, 53%);
  background: linear-gradient(15deg,hsl(34, 72%, 50%) 0%, hsl(56, 86%, 53%) 100%);
}

.darker {
  background: hsl(236, 91%, 58%);
  background: linear-gradient(15deg, hsl(0, 0%, 60%) 0%, hsl(0, 0%, 70%) 100%);
}

@media only screen and (min-width: 768px) {
  .calculator {
    width: 50vw;
    grid-auto-rows: minmax(7.5vh, auto);
    line-height: 7.5vh;
  }
}

@media only screen and (min-width: 1025px) {
  .calculator {
    width: 30vw;
  }
}

@media only screen and (min-width: 1281px) {
  .calculator {
    width: 20vw;
  }
}

@media only screen and (min-width: 1601px) {
  .calculator {
    width: 15vw;
  }
}
</style>

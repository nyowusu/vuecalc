<template>
  <div class="calculator">
    <div class="displays">
      <Displays :main="current" :auxilliary="auxilliary"></Displays>
    </div>
    <div class="buttons">
      <ClearScreen content="AC" v-on:clearScreen="clear($event)"></ClearScreen>
      <PlusMinus content="+/-" v-on:applyNegative="negateNumber($event)"></PlusMinus>
      <Percentage content="%" v-on:applyPercentage="percentage($event)"></Percentage>
      <OperatorButton operator="÷" v-on:setOperator="handleDivision($event)" class="right-buttons"></OperatorButton>
      <NumberButton number="7" v-on:appendNumber="append($event)"></NumberButton>
      <NumberButton number="8" v-on:appendNumber="append($event)"></NumberButton>
      <NumberButton number="9" v-on:appendNumber="append($event)"></NumberButton>
      <OperatorButton
        operator="x"
        v-on:setOperator="handleMultiplication($event)"
        class="right-buttons"
      ></OperatorButton>
      <NumberButton number="4" v-on:appendNumber="append($event)"></NumberButton>
      <NumberButton number="5" v-on:appendNumber="append($event)"></NumberButton>
      <NumberButton number="6" v-on:appendNumber="append($event)"></NumberButton>
      <OperatorButton
        operator="-"
        v-on:setOperator="handleSubtraction($event)"
        class="right-buttons"
      ></OperatorButton>
      <NumberButton number="1" v-on:appendNumber="append($event)"></NumberButton>
      <NumberButton number="2" v-on:appendNumber="append($event)"></NumberButton>
      <NumberButton number="3" v-on:appendNumber="append($event)"></NumberButton>
      <OperatorButton operator="+" v-on:setOperator="handleAddition($event)" class="right-buttons"></OperatorButton>
      <NumberButton number="0" v-on:appendNumber="append($event)" class="zero"></NumberButton>
      <NumberButton number="." v-on:appendNumber="append($event)"></NumberButton>
      <OperatorButton operator="=" v-on:setOperator="performOperation" class="right-buttons"></OperatorButton>
    </div>
  </div>
</template>

<script>
import Displays from "@/components/MainDisplay.component";
import Percentage from "@/components/PercentageButton.component";
import OperatorButton from "@/components/OperatorButton.component";
import NumberButton from "@/components/NumberButton.component";
import ClearScreen from "@/components/ClearScreenButton.component";
import PlusMinus from "@/components/PlusMinusButton.component";

export default {
  name: "Calculator",
  data() {
    return {
      current: "0",
      auxilliary: "0",
      prevValue: 0,
      operation: null,
    };
  },
  methods: {
    append: function(next_digit) {
      let current_number = this.current;
      let dot = ".";
      let string_zero = "0";
      let number_zero = 0;
      let minus_one = -1;

      if (next_digit == dot && current_number.indexOf(dot) > -1) {
        return;
      }

      if (
        current_number.indexOf(string_zero) == number_zero &&
        current_number.length == 1 &&
        next_digit != dot
      ) {
        current_number = "";
      }

      current_number += next_digit;
      this.current = current_number;
    },

    clear: function(val) {
      this.current = val;
      this.auxilliary = val;
    },

    negateNumber: function(sign) {
      this.current = String(this.current * sign);
    },

    percentage: function(rate) {
      this.current = String(this.current / rate);
    },

    handleAddition: function(operator) {
      // show current number in auxilliary display
      // with the addition sign
      // then clear main display.
      this.manageDisplays(operator);

      // set the operation function
      this.setOperation((prev, curr) => prev + curr);
    },

    handleSubtraction: function(operator) {
      // show current number in auxilliary display
      // with the minus sign
      // then clear main display.
      this.manageDisplays(operator);

      // set the operation function
      this.setOperation((prev, curr) => prev - curr);
    },

    handleMultiplication: function(operator) {
      // show current number in auxilliary display
      // with the multiplication sign
      // then clear main display.
      this.manageDisplays(operator);

      // set the operation function
      this.setOperation((prev, curr) => prev * curr);
    },

    handleDivision: function(operator) {
      // show current number in auxilliary display
      // with the multiplication sign
      // then clear main display.
      this.manageDisplays(operator);

      // set the operation function
      this.setOperation((prev, curr) => {
        if (curr == 0) {
          return "Math Error: cannot divide by zero";
        }

        return prev / curr;
      });
    },

    manageDisplays: function(operator) {
      // change only the sign
      if (this.auxilliary.length > 1 && this.auxilliary.lastIndexOf("0") != 0) {
        this.manageAuxilliaryDisplay(operator);
      } else if (
        (this.auxilliary.length == 1 &&
          (this.current.length == 1 && this.current.indexOf("0") != 0)) ||
        this.current.length > 1
      ) {
        // refresh the screen
        this.manageMainDisplay();
        this.manageAuxilliaryDisplay(operator);
      }
    },

    manageMainDisplay: function() {
      this.prevValue = Number(this.current);
      this.current = "0";
    },

    manageAuxilliaryDisplay: function(operator) {
      this.auxilliary = `${this.prevValue} ${operator} `;
    },

    setOperation: function(callback) {
      this.operation = callback;
    },

    performOperation: function() {
      let number = Number(this.current);

      if (this.operation != null) {
        number = this.operation(this.prevValue, number);
      }

      this.current = String(number);
      this.auxilliary = "0";
    },
  },
  components: {
    NumberButton,
    OperatorButton,
    Percentage,
    Displays,
    ClearScreen,
    PlusMinus,
  },
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  background-color: #6e6e6e;
  width: 90vw;
  height: 70vh;
  border-radius: 1rem;
  display: grid;
  grid-gap: 0.02rem;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(6, 1fr);
}
.displays {
  grid-column: 1 / 5;
  grid-row: 1 / 2;
}

.buttons {
  grid-column: 1 / 5;
  grid-row: 2 / 7;
  display: grid;
  grid-gap: 0.3rem;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(5, 1fr);
  border-radius: 1rem;
  padding: 0.2rem;
  justify-items: center;
  align-items: center;
}

.buttons > .zero {
  grid-column: 1 / 3;
}

.right-buttons {
  background-color: #ffa500;
}

@media only screen and (min-width: 760px) {
  .calculator {
    width: 50vw;
    height: 70vh;
    font-size: 20px;
    display: grid;
    grid-gap: 0.02rem;
  }
}

/* DESKTOP */
@media only screen and (min-width: 1350px) {
  .calculator {
    width: 30vw;
    height: 60vh;
  }
}
</style>



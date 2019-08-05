<template>
  <div class="calculator">
    <div class="displays"><Displays></Displays></div>
    <div class="buttons">
      <FunctionButton content="AC"></FunctionButton>
      <FunctionButton content="+/-"></FunctionButton>
      <FunctionButton content="%"></FunctionButton>
      <OperatorButton content="÷" class="right-buttons"></OperatorButton>
      <NumberButton content="7"></NumberButton>
      <NumberButton content="8"></NumberButton>
      <NumberButton content="9"></NumberButton>
      <OperatorButton content="x" class="right-buttons"></OperatorButton>
      <NumberButton content="4"></NumberButton>
      <NumberButton content="5"></NumberButton>
      <NumberButton content="6"></NumberButton>
      <OperatorButton content="-" class="right-buttons"></OperatorButton>
      <NumberButton content="1"></NumberButton>
      <NumberButton content="2"></NumberButton>
      <NumberButton content="3"></NumberButton>
      <OperatorButton content="+" class="right-buttons"></OperatorButton>
      <NumberButton content="0" class="zero"></NumberButton>
      <NumberButton content="."></NumberButton>
      <OperatorButton content="=" class="right-buttons"></OperatorButton>
    </div>
  </div>
</template>

<script>
import Displays from "@/components/MainDisplay.component";
import FunctionButton from "@/components/FunctionButton.component";
import OperatorButton from "@/components/OperatorButton.component";
import NumberButton from "@/components/NumberButton.component";

export default {
  name: "Calculator",
  components: { NumberButton, OperatorButton, FunctionButton, Displays },
  props: {
    msg: String
  }
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

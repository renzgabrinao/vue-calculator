<script>
import { def } from "@vue/shared";
import { calculatorButtons } from "./calulator-buttons";
export default {
  data() {
    return {
      input: "0",
      prevInput: "",
      currentOperand: "",
      buttons: calculatorButtons,
      OPERATORS: ["+", "-", "*", "/"],
    };
  },

  methods: {
    handleClick(button) {
      switch (button.type) {
        case "number":
          this.handleInput(button.value);
          break;
        case "operator":
          this.handleOperator(button.value);
          break;
        case "clear":
          this.handleClear();
          break;
        case "enter":
          this.handleCalculate();
          break;
        default:
          break;
      }
    },

    handleClear() {
      this.input = "0";
      this.prevInput = "";
      this.currentOperand = "";
    },

    handleInput(value) {
      if (this.input === "0") {
        this.input = value.toString();
      } else {
        this.input += value.toString();
      }
    },

    handleOperator(operator) {
      if (
        this.input !== "0" &&
        this.prevInput !== "" &&
        this.currentOperand !== ""
      ) {
        this.handleCalculate();
      }
      this.prevInput = this.input;
      this.currentOperand = operator;
      this.input = "0";
    },

    handleCalculate() {
      let prev = Number(this.prevInput);
      let current = Number(this.input);
      let result = 0;
      switch (this.currentOperand) {
        case "+":
          result = prev + current;
          break;
        case "-":
          result = prev - current;
          break;
        case "*":
          result = prev * current;
          break;
        case "/":
          result = prev / current;
          break;
        default:
          result = 0;
      }
      this.input = result.toString();
      this.currentOperand = "";
    },
  },

  mounted() {
    console.log("Hello Calculator");
  },
};
</script>

<template>
  <div class="main bg-black">
    <div class="pt-20 min-h-screen">
      <div
        class="h-20 w-[350px] px-6 mx-auto mb-7 text-right text-white flex items-end justify-end"
      >
        <h1 class="text-5xl">{{ this.input }}</h1>
      </div>
      <div
        class="grid grid-cols-4 text-center w-[350px] mx-auto justify-items-center gap-4"
      >
        <div
          class="h-20 w-20 flex justify-center items-center rounded-full text-3xl hover:scale-110 hover:cursor-pointer"
          :class="[item.class]"
          v-for="item in buttons"
          :key="item.className"
          @click="handleClick(item)"
        >
          <h1>{{ item.text }}</h1>
        </div>
      </div>
    </div>
    <footer>
      <h1 class="text-2xl pb-5 text-white font-mono font-bold text-center">
        &copy; Renz Gabrinao
      </h1>
    </footer>
  </div>
</template>

<style scoped></style>

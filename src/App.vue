<script>
  import {calculatorButtons} from './calulator-buttons';
  export default {
    data() {
      return {
        override: false,
        input: "0",
        prevInput: "",
        currentOperand: "",
        buttons: calculatorButtons,
        OPERATORS: ["+", "-", "*", "/"]
      }
    },

    methods: {
      handleClick(button) {
        console.log(`input: ${this.input}\nprevInput: ${this.prevInput}`);
        switch(button.type) {
          case "number":
            this.handleNumber(button.value);
            break;

          case "operator": 
            this.handleOperator(button.value);
            break;

          case "clear": 
            break;

          default: 
            break;
        }
      },

      handleNumber(num) {
        if(this.input === "0") {
          this.input = `${num}`
        }
        else {
          this.input = `${this.input}${num}`
        } 
      },

      handleOperator(operator) {
        
        if(this.input === "0" && this.prevInput === "") {
          return;
        }
        else if (this.input !== "0" && this.prevInput === "") {
          this.prevInput = this.input;
          this.input = "0";
          this.currentOperand = operator;
        }
        else if (this.input !== "0" && this.prevInput !== "") {
          this.currentOperand = operator;
          // calculate
          this.handleCalculate();
        }
      },  

      handleCalculate() {
        if(this.currentOperand !== "") {
          switch(this.currentOperand) {
            case "+":
              this.input = (Number(this.input) + Number(this.prevInput)).toString();
              this.prevInput = "";
              break;
            case "-":
              this.input = (Number(this.input) - Number(this.prevInput)).toString();
              this.prevInput = "";
              break;
            case "*":
              this.input = (Number(this.input) * Number(this.prevInput)).toString();
              this.prevInput = "";
              break;
            case "/":
              this.input = (Number(this.input) / Number(this.prevInput)).toString();
              this.prevInput = "";
              break;
          }
        }
      }



    },

    mounted() {
      console.log("Hello Calculator");
    }
  } 
  
</script>

<template>
  <div class="main bg-black min-h-screen pt-20">
    <div class="h-20 w-[350px] mx-auto mb-7 text-right text-white flex items-end justify-end">
      <h1 class="text-5xl">{{ this.input }}</h1>
    </div>
    <div class="grid grid-cols-4 text-center w-[350px] mx-auto justify-items-center gap-4">
      <div 
        class="h-20 w-20 flex justify-center items-center rounded-full bg-zinc-700 text-3xl hover:scale-110 hover:cursor-pointer" 
        :class="[item.class]" 
        v-for="item in buttons" 
        :key="item.className"
        @click="handleClick(item)"
      >
        <h1>{{ item.text }}</h1>
      </div>
    </div>

  </div>
</template>

<style scoped>

</style>

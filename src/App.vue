<template>
  <CalcView :content="calc_view_string" />
  <div id="button-div">
    <CalcButton :orange_color="true" content="1" @click="numberPress('1')" />
    <CalcButton :orange_color="true" content="2" @click="numberPress('2')" />
    <CalcButton :orange_color="true" content="3" @click="numberPress('3')" />
    <CalcButton content="+" @click="enableIsAdd" />
    <CalcButton :orange_color="true" content="4" @click="numberPress('4')" />
    <CalcButton :orange_color="true" content="5" @click="numberPress('5')" />
    <CalcButton :orange_color="true" content="6" @click="numberPress('6')" />
    <CalcButton content="-" @click="enableIsMinus" />
    <CalcButton :orange_color="true" content="7" @click="numberPress('7')" />
    <CalcButton :orange_color="true" content="8" @click="numberPress('8')" />
    <CalcButton :orange_color="true" content="9" @click="numberPress('9')" />
    <CalcButton content="x" @click="multiply" />
    <CalcButton :orange_color="true" content="0" @click="numberPress('0')" />
    <CalcButton content="Clear" @click="clear" />
    <CalcButton content="=" />
    <CalcButton content="/" />
  </div>
</template>

<script>
import CalcView from "./components/CalcView.vue";
import CalcButton from "./components/CalcButton.vue";

export default {
  name: "App",
  components: {
    CalcView,
    CalcButton,
  },
  data() {
    return {
      calc_view: [],
      calc_stack: [],
      is_add: true,
      is_minus: false,
    };
  },
  methods: {
    enableIsMinus() {
      this.is_minus = true;
      this.is_add = false;
    },
    enableIsAdd() {
      this.is_minus = false;
      this.is_add = true;
    },
    disableAll() {
      this.is_minus = false;
      this.is_add = false;
    },
    numberPress(value) {
      if (this.is_minus) this.subtractValue(value);
      else this.addValue(value);
    },
    addValue(value) {
      if (this.is_add) {
        this.calc_view.push("+" + value);
        this.disableAll();
      } else {
        this.calc_view.push(this.calc_view.pop() + value)
      }
    },
    subtractValue(value) {
      if (this.is_minus) {
        this.calc_view.push("-" + value);
        this.disableAll();
      } else {
        this.calc_view.push(this.calc_view.pop() + value)
      }
    },
    multiply() {
      if (!this.isOperator(this.calc_view[this.calc_view.length - 1])) {
        this.calc_view.push("*");
        this.enableIsAdd();
      }
    },
    clear() {
      this.calc_view = [];
      this.is_add = true;
    },
    isOperator(value) {
      return value.includes("*") || value.includes("/");
    },
  },
  computed: {
    calc_view_string: function () {
      let final_string = "";
      let show_signal = false;
      for (let index = 0; index < this.calc_view.length; index++) {
        const operation = this.calc_view[index];
        if (operation.includes("*") || operation.includes("/")) {
          show_signal = false;
          final_string += operation + " ";
        } else if (operation.includes("(")) {
          show_signal = false;
          final_string += " " + operation;
        } else if (operation.includes(")")) {
          final_string += operation + " ";
        } else if (show_signal == false && !operation.includes("-")) {
          final_string += operation.slice(1) + " ";
          show_signal = true;
        } else {
          final_string +=
            operation.slice(0, 1) + " " + operation.slice(1) + " ";

          show_signal = true;
        }
      }
      return final_string;
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  overflow-y: hidden;
  overflow-x: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#button-div {
  display: grid;
  height: 70vh;
  grid-template-columns: 25% 25% 25% 25%;
  grid-template-rows: 20% 20% 20% 20% 20%;

  margin: 10px;
}
</style>

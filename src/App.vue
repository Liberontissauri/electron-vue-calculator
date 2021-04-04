<template>
  <CalcView :content="calc_view_string" />
  <div id="button-div">
    <CalcButton :orange_color="true" content="1"/>
    <CalcButton :orange_color="true" content="2"/>
    <CalcButton :orange_color="true" content="3"/>
    <CalcButton content="+"/>
    <CalcButton :orange_color="true" content="4"/>
    <CalcButton :orange_color="true" content="5"/>
    <CalcButton :orange_color="true" content="6"/>
    <CalcButton content="-"/>
    <CalcButton :orange_color="true" content="7"/>
    <CalcButton :orange_color="true" content="8"/>
    <CalcButton :orange_color="true" content="9"/>
    <CalcButton content="x"/>
    <CalcButton :orange_color="true" content="0"/>
    <CalcButton content="Clear"/>
    <CalcButton content="="/>
    <CalcButton content="/"/>
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
      calc_view: ["+1", "+5"],
      calc_stack: [],
    };
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
  methods: {},
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

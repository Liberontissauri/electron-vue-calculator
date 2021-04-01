<template>
  <CalcView :content="calc_view_string" />
</template>

<script>
import CalcView from "./components/CalcView.vue";

export default {
  name: "App",
  components: {
    CalcView,
  },
  data() {
    return {
      calc_view: ["+1", "(", "-5", "(", "+5", "/", "-5", ")", ")", "+5"],
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
            operation.slice(0, 1) + " " + operation.slice(1, 2) + " ";

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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

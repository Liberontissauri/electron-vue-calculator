<template>
  <div class="CalcView-Div">
    <h2 class="CalcView-Content">{{ content }}</h2>
  </div>
</template>

<script>
export default {
  name: "CalcDisplay",
  props: {
    content: String,
  },
};
</script>

<style>
.CalcView-Div {
  display: flex;
  align-items: flex-end;
  height: 15vh;
  flex-direction: row-reverse;

  padding-bottom: 20px;
}
.CalcView-Content {
  margin-right: 40px;

  color: rgb(47, 47, 47);
  font-size: 24pt;
}
</style>

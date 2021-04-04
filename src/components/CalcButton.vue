<template>
  <div
    class="inside-button-div"
    v-bind:class="{
      'orange-button': orange_color,
      'grey-button': !orange_color,
    }"
  >
    <h2 class="button-text">{{ content }}</h2>
  </div>
</template>

<script>
export default {
  name: "CalcButton",
  props: {
    content: String,
    orange_color: Boolean,
  },
};
</script>

<style>
.inside-button-div {
  display: flex;
  justify-content: center;
  align-items: center;

  width: 90%;
  height: 90%;
  background-color: black;

  margin: 10px;

  opacity: 1;

  transition: 0.2s opacity ease-in;
}
.inside-button-div:hover {
  cursor: pointer;
  opacity: 0.7;
}
.orange-button {
  background-color: rgb(238, 158, 67);
  color: rgb(233, 223, 205);
}
.grey-button {
  background-color: rgb(233, 223, 205);
  color: rgb(121, 119, 116);
}
</style>

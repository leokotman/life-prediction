<template>
  <div>
    <p :class="styles">{{ header }}</p>
  </div>
</template>

<script>
export default {
  props: ["header", "styles"],
};
</script>

<style scoped>
div {
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  background: url("../assets/img/eye.svg") no-repeat bottom right;
}
p {
  max-width: 74%;
  margin: 0 auto 2.5rem;
  font-family: "Bad Script";
  font-style: normal;
  font-weight: normal;
  font-size: 0.875rem;
  line-height: 1.25rem;
  text-align: center;
}
.transparent {
  color: #fff;
  opacity: 0.6;
}
.window {
  background-color: #fff;
  border: 1px solid #fff;
  box-sizing: border-box;
  border-radius: 5px;
  position: relative;
  color: #202024;
  padding: .75rem;
}
.window:after,
.window:before {
  content: "";
  display: block;
  position: absolute;
  left: 90%;
  bottom: -20px;
  width: 0;
  height: 0;
  border-style: solid;
  border-color: #fff transparent transparent;
  border-width: 10px;
}
</style>

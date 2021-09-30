<template>
  <div class="quest_btn">
    <input type="button" :value="value" />
    <div class="btn-shine"></div>
  </div>
</template>

<script>
export default {
  props: ["value"],
};
</script>

<style scoped>
input {
  background: linear-gradient(
    90deg,
    rgba(246, 200, 102, 0.9) -6.2%,
    rgba(254, 173, 53, 0.9) 100%
  );
  border-radius: 50px;
  width: 100%;

  font-size: 0.875rem;
  line-height: 1rem;
  color: #fff;
  padding: 0.75rem 0;
}
.quest_btn {
  width: 56%;
  position: relative;
}
.btn-shine {
  width: 50%;
  height: 100%;
  position: absolute;
  top: 0;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
  -webkit-animation: slide-right 3s cubic-bezier(0.25, 0.46, 0.45, 0.94) 1s
    infinite forwards;
  animation: slide-right 3s cubic-bezier(0.25, 0.46, 0.45, 0.94) 1s infinite
    forwards;
}

@-webkit-keyframes slide-right {
  0% {
    -webkit-transform: translateX(-50px);
    transform: translateX(-50px);
  }
  100% {
    -webkit-transform: translateX(120%);
    transform: translateX(120%);
  }
}
@keyframes slide-right {
  0% {
    -webkit-transform: translateX(-50px);
    transform: translateX(-50px);
  }
  100% {
    -webkit-transform: translateX(120%);
    transform: translateX(120%);
  }
}
</style>

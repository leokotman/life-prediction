<template>
  <div>
    <img src="../assets/img/loading.png" alt="loading spinner" />
    <p>Loading</p>
  </div>
</template>

<style scoped>
div {
  min-height: 568px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
img {
  -webkit-animation: rotate-center 1s ease-in infinite both;
  animation: rotate-center 1s ease-in infinite both;
}
p {
  font-weight: 300;
  font-size: 12px;
  line-height: 14px;
  display: flex;
  align-items: center;
  text-align: center;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}

@-webkit-keyframes rotate-center {
  0% {
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
@keyframes rotate-center {
  0% {
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>

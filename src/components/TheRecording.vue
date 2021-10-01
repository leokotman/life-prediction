<template>
  <section>
    <img src="../assets/img/recording.png" alt="запись сообщения" />
    <div>
      <span class="progress-bar" :style="'width:' + barWidth"></span>
    </div>
    <p class="progress">{{ barWidth }}</p>
    <p class="recording_msg">Запись сообщения</p>
  </section>
</template>

<script>
export default {
  data() {
    return {
      barWidth: "",
    };
  },
  emits: ["recorded"],
  methods: {
    changeProgress() {
      let width = 1;
      let progress = setInterval(() => {
        if (width >= 100) {
          clearInterval(progress);
        } else {
          width++;
          this.barWidth = width + "%";
        }
      }, 30);
    },
  },
  watch: {
    barWidth() {
      if (this.barWidth == "100%") {
        this.$emit("recorded");
      }
    }
  },
  mounted() {
    this.changeProgress();
  },
};
</script>

<style scoped>
section {
  height: 200px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
div {
  background-color: #fff;
  width: 81%;
  border-radius: 5px;
}

div span {
  background-color: #f6c866;
  border-radius: 5px;
  display: block;
  height: 0.3rem;
  max-width: 100%;
}
.progress {
  font-weight: 300;
  font-size: 1.25rem;
  line-height: 143%;
  color: rgba(255, 255, 255, 0.6);
}
.recording_msg {
  font-weight: 300;
  font-size: 0.75rem;
  line-height: 0.875rem;
  color: rgba(255, 255, 255, 0.6);
}
</style>

<template>
  <section>
    <p class="cloud">
      Спасибо за Ваши ответы!
      <span
        >Мы подготовили для Вас персональную аудио запись с Вашим
        прогнозом.</span
      >
    </p>
    <p class="txt">
      Вы можете узнать, как повлиять на события, которые ожидают вас в ближайшем
      будущем.
    </p>
    <div class="card">
      <span
        >Первое значимое событие может произойти уже {{ tomorrowDate }},</span
      >
      вам надо быть готовым, чтобы последствия не оказались необратимыми.
    </div>
    <p class="txt">
      Нажмите на кнопку ниже прямо сейчас и наберите наш номер телефона.
      Прослушайте важную информацию!
    </p>
    <the-button
      @click.native="getData"
      :value="'Позвонить и прослушать'"
      :btnColor="'green_btn'"
    />
    <ul>
      <li v-for="(data, idx) in receivedData" :key="data.idx">
        {{ idx }} - {{ data }}
      </li>
    </ul>
  </section>
</template>

<script>
import TheButton from "./TheButton.vue";

export default {
  components: { TheButton },
  props: ["receivedData"],
  emits: ["getData"],
  data() {
    return {
      tomorrowDate: "",
    };
  },
  methods: {
    getData() {
      this.$emit("getData");
      console.log("predictResults emitted");
    },
    getTomorrowDate() {
      let currentDate = new Date(new Date().getTime() + 24 * 60 * 60 * 1000);
      let day = currentDate.getDate();
      let month = currentDate.getMonth() + 1;
      let year = currentDate.getFullYear();
      this.tomorrowDate = day + "." + month + "." + year;
    },
  },
  mounted() {
    this.getTomorrowDate();
  },
};
</script>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.cloud {
  background-color: #fff;
  border: 1px solid #fff;
  box-sizing: border-box;
  border-radius: 5px;
  position: relative;
  color: #202024;
  width: 80%;
  max-width: 259px;
  margin: 0 auto;
  font-size: 0.875rem;
  font-weight: 400;
  line-height: 129%;
  text-align: center;
}
.cloud span {
  font-weight: 700;
}
.cloud:after,
.cloud:before {
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
.txt {
  font-weight: 300;
  font-size: 0.875rem;
  line-height: 1rem;
  text-align: center;
  text-transform: uppercase;
  color: #fff;
  max-width: 230px;
}

.card {
  border: 1px solid #fff;
  box-sizing: border-box;
  border-radius: 3px;
  width: 80%;
  padding: 0.8rem;
  font-weight: 400;
  font-size: 1rem;
  line-height: 156%;
  color: #f6c866;
}
.card span {
  font-weight: 700;
  text-transform: uppercase;
}
li {
  color: white;
  list-style-type: none;
}
</style>

<template>
  <div>
    <p>Спасибо за Ваши ответы!
Мы подготовили для Вас персональную аудио запись с Вашим прогнозом.
</p>
<p>Вы можете узнать, как повлиять на события, которые ожидают вас в ближайшем будущем. 
</p>
<div>Первое значимое событие может произойти уже {{}}, Вам надо быть готовым, что бы последствия не оказались необратимыми.
</div>
    <button @click="getData">Позвонить и прослушать</button>
    <ul>
      <li v-for="(data, idx) in receivedData" :key="data.idx">
        {{ idx }} - {{ data }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["receivedData"],
  emits: ["getData"],
  data() {
      return {
          tomorrowDate: "",
      }
  },
  methods: {
    getData() {
      this.$emit("getData");
      console.log("predictResults emitted");
    },
  },
};
</script>

<style scoped>
li {
  color: white;
  list-style-type: none;
}
</style>

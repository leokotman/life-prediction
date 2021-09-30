<template>
  <section>
    <div v-show="questions[currentQuestion]">
      <predict-header
        v-show="questions[currentQuestion].header"
        :header="questions[currentQuestion].header"
      />
      <p>{{ questions[currentQuestion].text }}</p>
      <ul v-for="answer in questions[currentQuestion].answers" :key="answer">
        <li v-if="questions[currentQuestion].type === 'button'">
          <the-button :value="answer" @click.native="handleAnswerClick" />
        </li>
        <li v-else>
          <form>
            <div v-if="answer === 'День'">
              <select name="day" id="" required>
                <option value="День">День</option>
                <option value="1">1</option>
                <option value="2">2</option>
              </select>
            </div>
            <div v-else-if="answer === 'Месяц'">
              <select name="month" id="" required>
                <option value="Месяц">Месяц</option>
                <option value="1">Январь</option>
                <option value="2">Февраль</option>
                <option value="3">Март</option>
                <option value="4">Апрель</option>
                <option value="5">Май</option>
                <option value="6">Июнь</option>
                <option value="7">Июль</option>
                <option value="8">Август</option>
                <option value="9">Сентябрь</option>
                <option value="10">Октябрь</option>
                <option value="11">Ноябрь</option>
                <option value="12">Декабрь</option>
              </select>
            </div>
            <div v-else>
              <input
                type="number"
                min="1900"
                max="2008"
                name="year"
                placeholder="Год"
                required
              />
            </div>
              <the-button :value="'Далее'" @click.native="handleAnswerClick" />
          </form>
        </li>
      </ul>

      <span>вопрос № {{ currentQuestion + 1 }} - 5</span>
    </div>
    <!-- компонент -->
    <div v-if="isLoading">loading spinner</div>
    <!-- компонент -->

    <div v-if="isRecording">Запись сообщения</div>
  </section>
</template>

<script>
import PredictHeader from "./PredictHeader.vue";
import TheButton from "./TheButton.vue";

export default {
  components: {
    PredictHeader,
    TheButton,
  },
  data() {
    return {
      isLoading: false,
      isRecording: false,
      currentQuestion: 0,
      questions: [
        {
          text: "Боитесь ли вы умереть?",
          answers: ["Да", "Нет"],
          type: "button",
          header: "",
        },
        {
          text: "Когда Вы чувствуете себя наиболее комфортно?",
          answers: ["Утро", "День", "Вечер", "Ночь"],
          type: "button",
          header:
            "Мы расскажем Вам не только подробности вашей смерти, но также поможем Вам избежать этой ужасной даты и продлить вашу жизнь на многие годы.",
        },
        {
          text: "Укажите свою дату рождения:",
          answers: ["День", "Месяц", "Год"],
          type: "select",
          header:
            "Уже совсем скоро Вы узнаете много интересного о своем будущем!",
        },
        {
          text: "Снятся ли Вам умершие люди?",
          answers: ["Да", "Нет", "Иногда"],
          type: "button",
          header:
            "Смерть родного человека – одно из тяжелейших испытаний в жизни каждого из нас!",
        },
        {
          text: "Запись, которую Вы услышите, может шокировать людей с неокрепшей психикой. Вы готовы узнать, что ждет именно Вас?",
          answers: ["Да", "Затрудняюсь ответить"],
          type: "button",
          header: {
            "18-35":
              "По вам скучает очень близкий человек, которого больше нет в мире живых",
            "36-45":
              "По вам скучает очень близкий человек, которого больше нет в мире живых. Возможно это дедушка или бабушка",
            "46+":
              "По вам скучает очень близкий человек, которого больше нет в мире живых. Возможно это кто-то из Ваших родителей",
          },
        },
      ],
    };
  },
  methods: {
    handleAnswerClick() {
      let nextQuestion = this.currentQuestion + 1;
      if (nextQuestion < this.questions.length) {
        this.currentQuestion = nextQuestion;
      } else {
        this.isRecording = true;
      }
    },
  },
};
</script>

<style scoped>
select {
  width: 100px;
  height: 30px;
}
select option {
  height: 30px;
}
</style>

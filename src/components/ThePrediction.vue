<template>
  <section>
    <div
      v-if="currentQuestion <= 4 && !isLoading && !isRecording"
      class="prediction_div"
    >
      <predict-header
        v-show="questions[currentQuestion].header"
        :header="questions[currentQuestion].header"
        :styles="headerClass"
      />
      <p class="question">{{ questions[currentQuestion].text }}</p>
      <div v-for="answer in questions[currentQuestion].answers" :key="answer">
        <li v-if="questions[currentQuestion].type === 'button'">
          <the-button :value="answer" @click.native="handleAnswerClick" />
        </li>
        <li v-else>
          <div v-if="answer === 'День'">
            <select name="day" id="" v-model="birthDay">
              <option value="День" disabled>День</option>
              <option value="1">1</option>
              <option value="2">2</option>
            </select>
          </div>
          <div v-else-if="answer === 'Месяц'">
            <select name="month" id="" v-model="birthMonth">
              <option value="Месяц" disabled>Месяц</option>
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
              v-model="birthYear"
            />
          </div>
        </li>
      </div>
      <the-button
        v-if="questions[currentQuestion].type === 'select'"
        :value="'Далее'"
        @click.native="calculateAge"
      />
      <span>вопрос № {{ currentQuestion + 1 }} - 5</span>
    </div>

    <the-loading v-else-if="isLoading" />

    <the-recording v-if="isRecording" @recorded="showFinalStage" />
    <predict-results
      v-if="resultsShown"
      @getData="getData"
      :receivedData="receivedData"
    />
  </section>
</template>

<script>
import PredictHeader from "./PredictHeader.vue";
import PredictResults from "./PredictResults.vue";
import TheButton from "./TheButton.vue";
import TheLoading from "./TheLoading.vue";
import TheRecording from "./TheRecording.vue";

export default {
  components: {
    PredictHeader,
    TheButton,
    TheLoading,
    TheRecording,
    PredictResults,
  },
  data() {
    return {
      isLoading: false,
      isRecording: false,
      resultsShown: false,
      headerClass: "transparent",
      birthDay: null,
      birthMonth: null,
      birthYear: null,
      currentQuestion: 0,
      clientAge: 0,
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
      clientAnswers: [],
    };
  },
  props: ["receivedData"],
  emits: ["hideFooter", "getData"],
  methods: {
    handleAnswerClick(e) {
      let targetBtn = e.target.parentNode.querySelector("input");
      if (this.currentQuestion === 0) {
        this.$emit("hideFooter", true);
      }
      let nextQuestion = this.currentQuestion + 1;

      console.log(targetBtn.value);
      this.saveResults(targetBtn.value);

      if (nextQuestion < this.questions.length) {
        this.currentQuestion = nextQuestion;
      } else {
        this.isRecording = true;
      }
    },
    calculateAge(e) {
      if (!this.birthDay || !this.birthMonth || !this.birthYear) {
        alert("Заполните для продолжения, пожалуйста, все поля даты рождения");
      } else {
        this.isLoading = true;
        this.clientAge = new Date().getFullYear() - this.birthYear;
        this.saveResults({
          birthDay: this.birthDay,
          birthMonth: this.birthMonth,
          birthYear: this.birthYear,
        });

        setTimeout(() => {
          this.isLoading = false;
          this.handleAnswerClick(e);
        }, 2500);
      }
    },
    saveResults(result) {
      this.clientAnswers.push(result);
    },
    showFinalStage() {
      this.currentQuestion++;
      this.isRecording = false;
      this.resultsShown = true;

      this.$emit("hideFooter", false);
    },
    getData() {
      this.$emit("getData");
      console.log("thePrediction emitted");
    },
  },
  watch: {
    currentQuestion() {
      if (this.currentQuestion === 4) {
        return (this.headerClass = "window");
      }
    },
  },
};
</script>

<style scoped>
.prediction_div {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.prediction_div span {
  font-weight: 300;
  font-size: 0.75rem;
  line-height: 0.875rem;
  text-align: center;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.prediction_div li {
  list-style-type: none;
}

.question {
  font-size: 1rem;
  line-height: 156%;
  text-align: center;
  text-transform: uppercase;
  color: #f6c866;
}

select {
  width: 100px;
  height: 30px;
}
select option {
  height: 30px;
}
</style>

<template>
  <div id="app">
    <header id="header">
      <h1>Лучшие астрологи и экстрасенсы Румынии</h1>
      <h2>Точность прогноза: 97%</h2>
      <div class="header_imgs">
        <img
          src="./assets/img/face.png"
          alt="woman"
          class="face_img"
          width="137"
        />
        <img
          src="./assets/img/icon1.svg"
          alt="icon1"
          class="icon_circle"
          width="225"
        />
      </div>
      <div class="header_quest">
        <p>
          Вас беспокоит вопрос о том,
          <span>когда Вы покинете этот Мир и при каких обстоятельствах?</span>
        </p>

        <the-button
          @click.native="scrollPage('the_prediction')"
          :value="'Да'"
        ></the-button>
        <the-button
          @click.native="scrollPage('main')"
          :value="'Нет'"
        ></the-button>
        <h4>Онлайн предсказание</h4>
      </div>
    </header>

    <main id="main">
      <section class="promo_card">
        <img src="./assets/img/hands.png" alt="hands" />
        <p>
          Позвольте нам раскрыть эту волнующую тайну и
          <span>с точностью определить дату и время вашей смерти,</span> а также
          предшествующую этому событию причину
        </p>
      </section>
      <section class="promo_txt">
        <p>
          Многие не верят предсказаниям и мы решили доказать каждому,
          <span>что прогноз может изменить жизнь любого человека!</span>
        </p>
      </section>
      <div>
        <the-prediction id="the_prediction">
          <button @click="getData">Позвонить и прослушать</button>
        </the-prediction>
      </div>
    </main>

    <footer>
      <div v-show="!footerHidden">
        <img src="" alt="руны" />
        <p>Вы, конечно, умрете. И все, с кем вы знакомы, тоже однажды умрут.</p>
        <img src="" alt="руны" />
      </div>
      <p>
        TERMENI SI CONDITII: ACESTA ESTE UN SERVICIU DE DIVERTISMENT. PRIN
        FOLOSIREA LUI DECLARATI CA AVETI 18 ANI IMPLINITI,
      </p>
    </footer>
  </div>
</template>

<script>
import TheButton from "./components/TheButton.vue";
import ThePrediction from "./components/ThePrediction.vue";

export default {
  name: "App",
  components: { ThePrediction, TheButton },
  data() {
    return {
      footerHidden: false,
    };
  },
  methods: {
    async getData() {
      try {
        let response = await fetch("https://swapi.dev/api/people/1/");
        const people = await response.json();
        console.log(people);
        this.footerHidden = true;
      } catch (error) {
        console.log(error);
      }
    },

    scrollPage(id) {
      console.log("btn clicked to scroll");
      let targetSection = document.getElementById(id);
      targetSection.scrollIntoView({ behavior: "smooth" });
    },
  },
};
</script>

<style>
@import "./styles/fonts.css";

html,
body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: black;
  text-align: center;
  color: #fff;
}
#header {
  min-height: 568px;
  background-image: url("./assets/img/blik.png");
  background-position: center;
  background-repeat: no-repeat;
}
#header h1 {
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  margin: 0;
  padding: 0.8rem 0;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.75rem;
  font-weight: 300;
  line-height: 0.875rem;
  letter-spacing: 0.1em;
  text-align: center;
}
#header h2 {
  margin: 0.5rem 0 0;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 300;
  font-size: 1.25rem;
  line-height: 1.4375rem;
  text-align: center;
  letter-spacing: 0.1em;
}
.header_imgs {
  position: relative;
  height: 225px;
  width: 225px;
  margin: 2.3rem auto 0;
}
.face_img {
  position: absolute;
  top: 20%;
  left: 20%;
}

.header_quest {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.header_quest p {
  font-size: 1rem;
  line-height: 156%;
  text-align: center;
  color: #f6c866;
  margin: 0;
  padding: 1.5rem;
}
.header_quest p > span {
  text-transform: uppercase;
}

.header_quest .quest_btn:first-of-type {
  margin-bottom: 1.25rem;
}

.header_quest h4 {
  font-weight: 300;
  font-size: 0.75rem;
  line-height: 0.875rem;
  text-align: center;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
  margin: 1.25rem 0;
}

#main .promo_card {
  position: relative;
  border: 1px solid #fff;
  box-sizing: border-box;
  border-radius: 3px;
  width: 80%;
  margin: 19% auto 0;
  padding: 18% 1.5rem 2rem;

  font-weight: 400;
  font-size: 1rem;
  line-height: 156%;
}
.promo_card img {
  position: absolute;
  width: 25%;
  left: 40%;
  top: -35px;
}
.promo_card span {
  color: rgb(246, 200, 102);
  font-weight: 500;
  font-size: 1.25rem;
  line-height: 156%;
}

#main .promo_txt {
  background: linear-gradient(rgba(0, 0, 0.2), rgba(0, 0, 0, 0.2)),
    url("./assets/img/image-7.jpeg") no-repeat;
  background-position-y: center;
  background-position-x: -28vw;
  min-height: 330px;

  display: flex;
  justify-content: center;
  align-items: center;
}
.promo_txt p {
  font-size: 1rem;
  line-height: 156%;
  font-weight: 400;
  max-width: 69%;
}
.promo_txt p > span {
  font-size: 1.25rem;
  color: rgb(246, 200, 102);
}
</style>

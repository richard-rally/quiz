<template>
  <div id="app">

    <h2 class="mb-4">Quiz</h2>

    <ul>

      <div class="mb-4">
        <h3>Rounds:</h3>
        <ul>
          <li v-for="(round, index) in rounds" :key="index">
            {{ index + 1 }}: <a @click="roundIndex = index" href="#">{{ round.title }}</a>
          </li>
        </ul>
      </div>

      <QuestionGroup :round="selectedRound"></QuestionGroup>

    </ul>

  </div>
</template>

<script>

import QuestionGroup from "@/components/QuestionGroup";
// import json from "@/questions/2020-05-01";
import axios from 'axios';


export default {
  name: 'App',
  components: {QuestionGroup},

  computed: {
    selectedRound () {
      return this.rounds[this.roundIndex];
    }
  },

  created() {
      this.getQuiz().then((response) => {

          this.rounds = response.data.data.rounds;

          // console.log(response.data.data)
      });
  },

  data () {
    return {
      roundIndex: 0,
      rounds: []
    }
  },

  methods : {

    getQuiz () {

      return axios.get('http://quiz-api.test/api/quizzes/ddb6f4ec-292e-4513-b342-0479eabe751c');

    },

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

p {
  width: auto;
}

  ul {
    padding-left: 0;
  }

  ul li {
    padding-left: 0;
    list-style-type: none;
  }
</style>

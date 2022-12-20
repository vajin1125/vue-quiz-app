<template>
  <div id="app">
    <article>
        <header>
          <h1>How good are you at front-end development?</h1>
        </header>

        <template v-if="!isEnd">
          <section>
              <p>Question {{ currentQuestion + 1 }} out of {{ questions.length }}</p>
              <Question :question="questions[currentQuestion]" @nextQuestion="nextQuestion" />
          </section>
        </template>

        <template v-else>
          <Result :result="result" />
        </template>

    </article>
  </div>
</template>

        
<!-- <script>
    export default {
        name: 'ComponentName', // The name of the current component
        components: {}, // Other components included in the current component. If there are no child components, you can use the props property to set the basic parameters
        data() {}, // Objects that will be used to fill elements with data
        watch: {}, // The property that observes and reacts to data changes based on some other data
        computed: {}, // Computed properties
        methods: {} // Custom methods
    }
</script> -->
    

<script>
  // Import components
  import Question from './components/Question';
  import Result from './components/Result';

  export default {
    name: 'App',

    components: {
      Question,
      Result
    },

    // The data() method will return objects with questions and answers
    data() {
      return {
        questions      : [
            {
                title  : 'What is CSS?',
                answers: [
                    {text: 'Controlled Sporadic Spasms'},
                    {text: 'Critical Stylish Severity'},
                    {text: 'Cascading Style Sheets', isCorrect: true},
                ],
            },
            {
                title  : 'What is not a front-end  tool?',
                answers: [
                    {text: 'Webpack'},
                    {text: 'Tortilla', isCorrect: true},
                    {text: 'Gulp'},
                ],
            },
            {
                title  : 'What is an HTML tag for an ordered list?',
                answers: [
                    {text: '<ol>', isCorrect: true},
                    {text: '<list>'},
                    {text: '<ul>'},
                ],
            },
        ],
        currentQuestion: 0,
        correctAnswers : 0,
      };
    },

    computed: {
      isEnd() {
        return this.questions.length <= this.currentQuestion;
      },

      result() {
        return Math.round((this.correctAnswers / this.questions.length) * 100);
      }
    },

    // nextQuestion() will increment the counter of correct answers (correctAnswers) if the answer submitted by the user is correct
    methods: {
      nextQuestion(answer) {
        if (answer.isCorrect) {
            this.correctAnswers++;
        }

        this.currentQuestion++;
      }
    },
  };
</script>
    

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

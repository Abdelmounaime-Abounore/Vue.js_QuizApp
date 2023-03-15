<script setup>
  import {ref, computed} from 'vue'
  const questions = ref([
    {
      question: 'Using which of the following way can you embed PHP code in an HTML page?',
      answer: 3,
      options: [
        'A - <php PHP code goes here ?>',
        'B - < PHP code goes here ?>',
        'C - <script language="php"> PHP code goes here < /script>',
        'D - All of the above.'
      ],
      selected: null
    },
    {
      question: 'Which of the following is correct about constants vs variables in PHP?',
      answer: 2,
      options: [
      "A - There is no need to write a dollar sign ($) before a constant, where as in Variable one has to write a dollar sign.",
      "B - Constants cannot be defined by simple assignment, they may only be defined using the define() function.",
      "C - Both of the above.",
      "D - None of the above."
      ],
      selected: null
    },
    {
      question: "Which of the following function is used to locate a string within a string?",
      answer: 2,
      options: [
      "A - search()", 
      "B - locate()",
      "C - strpos()",
      "D - None of the above."
      ],
      selected: null
    },
    {
      question: "How will you concatenate two strings?",
      answer: 0,
      options: [
      "A - Using . operator.",
      "B - Using + operator.",
      "C - Using add() function", 
      "D - Using append() function"
      ],
      selected: null
    },
    {
      question: "Which of the following is used to check if session variable is already set or not in PHP?",
      answer: 2,
      options: [
      "A - session_start() function", 
      "B - $_SESSION[]", 
      "C - isset() function", 
      "D - session_destroy() function"
      ],
      selected: null
    },
    {
      question: "Which of the following is an array containing information such as headers, paths, and script locations?",
      answer: 1,
      options: [
      "A - $GLOBALS", 
      "B - $_SERVER", 
      "C - $_COOKIE", 
      "D - $_SESSION"
      ],
      selected: null
    },
    {
      question: "Which of the following gives a string containing PHP script file name in which it is called?",
      answer: 0,
      options: [
      "A - $_PHP_SELF", 
      "B - $php_errormsg", 
      "C - $_COOKIE", 
      "D - $_SESSION"
      ],
      selected: null
    },
    {
      question: "Which of the following method connect a MySql database using PHP?",
      answer: 0,
      options: [
      "A - mysql_connect()", 
      "B - mysql_query()", 
      "C - mysql_close()", 
      "D - None of the above"
      ],
      selected: null
    },
    {
      question: "Which of the following variables is not a predefined variable?",
      answer: 1,
      options: [
      "A - $get", 
      "B - $ask", 
      "C - $request", 
      "D - $post"
      ],
      selected: null
    },
    {
      question: "When you need to obtain the ASCII value of a character which of the following function you apply in PHP?",
      answer: 2,
      options: [
      "A - chr( );", 
      "B - asc( );", 
      "C - ord( );", 
      "D - val( );"
      ],
      selected: null
    },
  ])
  const quizCompleted = ref(false)
  const currentQuestion = ref(0)
  const score = computed(() => {
    let value = 0
    questions.value.map((q) => {
      if(q.selected == q.answer) {
        value++
      }
    })
    return value
  })
  const getCurrentQuestion = computed(() => {
    let question = questions.value[currentQuestion.value]
    question.index = currentQuestion.value
    return question
  })
  const setAnswer = evt => {
    questions.value[currentQuestion.value].selected = evt.target.value
    evt.target.value = null
  }
  const nextQuestion = () => {
    if (currentQuestion.value < questions.value.length - 1){
      currentQuestion.value ++
    } else {
      quizCompleted.value = true
    }
  }
</script>

<template>
  <main class="app">
    <h1>PHP Knowledge</h1>
    <div class="quiz" v-if="!quizCompleted">
      <span class="question">{{ getCurrentQuestion.question }}</span>
      <div class="options">
        <label 
          v-for="(option, index) in getCurrentQuestion.options" :key="index"
          :class="`option ${
            getCurrentQuestion.selected == index
            ? index == getCurrentQuestion.answer
            ? 'correct'
            : 'wrong'
            : '' 
          } ${
            getCurrentQuestion.selected != null && index != getCurrentQuestion.selected ? 'disabled' : ''
          }`">
          <input type="radio" 
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="setAnswer">
          <span class="answers">{{ option }}</span>
        </label>
      </div>
      <div class="btn">
        <button @click="nextQuestion" :disabled="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length - 1
            ? 'Finish'
            : getCurrentQuestion.selected == null
              ? 'Select an Option'
              : 'Next Question'
        }}
       </button>
        <span class="score">{{ score }} / {{ questions.length }}</span>
      </div>
    </div>
    
    <div v-else>
      <h2>You have finished the Quiz</h2>
      <p style="color: red; font-weight: bold;">Your score is {{ score }} / {{ questions.length }}</p>
    </div>
  </main>
</template>

<style>
  body {
    background-color: rgb(220, 216, 224);
    color: rgb(80, 79, 79);
  }
  h1{
    margin-top: 0px;
  }
  .quiz{
    margin-top: 60px;
    background-color: rgb(211, 207, 207);
    border-radius: 7px;
    padding: 17px;
  }
  .question {
      font-size: 25px;
      font-weight: bold;
      color: gray;
  }
  .options {
    margin-top: 25px;
  }
  .option {
    display: flex;
    flex-direction: row;
    align-items: center;
    margin-top: 10px;
  }
  .answers{
    margin-left: 5px  ;
  }
  .btn {
    display: flex;
    justify-content: space-between;
    margin-top: 22px;
  }
  .score {
    font-weight: bold;
    color: red;
  }
</style>

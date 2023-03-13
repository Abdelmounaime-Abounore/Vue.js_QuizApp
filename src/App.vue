<script setup>
  import {ref, computed} from 'vue'
  const questions = ref([
    {
      question: 'what is vue?',
      answer: 0,
      options: [
        'Is a framwork',
        'Is a Tagine',
        'Is Contry'
      ],
      selected: null
    },
    {
      question: 'what is php?',
      answer: 0,
      options: [
        'Is a langage',
        'Is a city',
        'Is street'
      ],
      selected: null
    },
    {
      question: 'what is js?',
      answer: 0,
      options: [
        'Is a langafe',
        'Is a chihaja',
        'Is Contry'
      ],
      selected: null
    }
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
  <h1>Test</h1>
</template>

<style>
  body {
    background-color: rgb(42, 8, 75);
    color: white;
  }
</style>

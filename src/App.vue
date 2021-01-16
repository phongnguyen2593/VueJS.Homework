<template>
  <div id="app">
    <!-- Start Homework Unit 2 -->
    <!-- <HomeworkUnit02 /> -->
    <!-- End Homework Unit 2 -->
    
    <!-- Start Homework Unit 3 -->
    <!-- <Todo /> -->
    <Exercise />
    <!-- End Homework Unit 3 -->

  </div>
</template>

<script>
// import HomeworkUnit02 from './components/Homework/Unit02.vue'

// import Todo from './components/Homework/Unit03/Exercise01/Todo.vue'
import Exercise from './components/Homework/Unit03/Exercise02/Exercise.vue'

export default {
  name: 'App',
  components: {
    // HomeworkUnit02

    // Unit 3
    // Todo,
    Exercise

  }
}
</script>

<style lang="scss">

// body {
  /* CSS Unit 3 Exercise 1 */
  // background-color: #0080DD;

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;

  }
// }
</style>

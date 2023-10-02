<template>
  <div class="ctr">
    <transition-group name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition-group>
    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "If January = 717, March = 5315 and June = 4624 then what does August equal?",
          answers: [
            {
              text: "6848",
              is_correct: true,
            },
            {
              text: "6432",
              is_correct: false,
            },
            {
              text: "6876",
              is_correct: false,
            },
            {
              text: "6543",
              is_correct: false,
            },
          ],
        },
        {
          q: 'Read this sentence carefully and then read it back. What is the missing word? Was it a *** or a cat I saw?',
          answers: [
            {
              text: "cat",
              is_correct: false,
            },
            {
              text: "saw",
              is_correct: false,
            },
            {
              text: "car",
              is_correct: true,
            },
            {
              text: "missing",
              is_correct: false,
            },
          ],
        },
        {
          q: "If the 3rd of March, 8th of November and 9th September are all the same, then what in October is also the same?",
          answers: [
            {
              text: "6th",
              is_correct: false,
            },
            {
              text: "7th",
              is_correct: true,
            },
            {
              text: "8th",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },

    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style></style>

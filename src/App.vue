<template>
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import axios from "axios"

export default defineComponent({
  name: "App",
  data() {
    return {
      dquestion: "",
      answer: "Questions usually contain a question mark. ;-)"
    }
  },
  computed: {
    question: {
      get(): string {
        return this.dquestion
      },
      set(newQ) {
        this.dquestion = newQ
        if (newQ.indexOf("?") > -1) {
          this.getAnswer()
        }
      }
    }
  },
  methods: {
    getAnswer() {
      this.answer = "Thinking..."
      axios
        .get("https://yesno.wtf/api")
        .then(response => {
          this.answer = response.data.answer
        })
        .catch(error => {
          this.answer = "Error! Could not reach the API. " + error
        })
    }
  }
})
</script>

<style scoped></style>

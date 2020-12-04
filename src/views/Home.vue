<template>
  <div class="question-form">
    <form name="ask-question" netlify enctype="application/x-www-form-urlencoded" netlify-honeypod="bot-field" method="post" @submit.prevent="handleSubmit">
      <input type="hidden" name="form-name" value="ask-question" />
        <label>
          Your Name:
          <input
            type="text"
            name="name"
            @input="ev => form.name = ev.target.value"
            >
        </label>
        <label>
          Your Question:
          <textarea
             ref="input"
             name="question"
             @input="ev => form.question = ev.target.value"
             placeholder="Question Goes Here"
          />
        </label>
      <button type="submit" class="submit-button">Ask a question</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "question-form",
  data() {
    return {
      form: {
        name: "",
        question: ""
      },
    };
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    handleSubmit() {
      fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": "ask-question",
          ...this.form
        })
      })
        .then(() => {
          this.$router.push("about");
        })
        .catch(() => {
          this.$router.push("about");
        });
    }
  }
};
</script>
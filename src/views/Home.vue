<template>
  <div class="question-form">
    <form method="post" @submit.prevent="handleSubmit">
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
      panelists: ["Chris Fritz", "Evan You", "Both"],
      form: {
        askPerson: "Chris Fritz",
        name: "",
        question: ""
      },
      sent: false,
      status: {}
    };
  },
  methods: {
    ifEvan(person) {
      return person === "Evan You" || person === "Both";
    },
    removeNotification() {
      this.sent = false;
    },
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
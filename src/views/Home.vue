<template>
  <div>
    <form  @submit.prevent="onSubmit">
      <input type="text" v-model="name" name="name" >
      <input type="email" v-model="email" name="email">
      <textarea v-model="content" name="content"></textarea>

      <button type="submit">送信</button>
    </form>


    <form name="contact" netlify netlify-honeypot="bot-field" hidden>
      <input type="text" name="name" />
      <input type="email" name="email" />
      <textarea name="content"></textarea>
    </form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      name: '',
      email: '',
      content: '',
    }
  },
  methods: {
    onSubmit() {
      const params = new URLSearchParams()

      params.append('form-name', 'contact') // Forms使うのに必要

      params.append('name', this.name)
      params.append('email', this.email)
      params.append('content', this.content)

      axios
        .post('/', params)
        .then(() => {
          this.$router.push("about");
        })
    }
  }
}
</script>
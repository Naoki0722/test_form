<template>
  <div class="home">
    <form name="contact" method="POST" netlify netlify-honeypot="bot-field">
      <input type="hidden" name="form-name" value="contact" />
      <label>名前</label>
      <input type="text" name="name" />
      <label>メールアドレス</label>
      <input type="text" name="email" />
      <label>お問い合わせ内容</label>
      <textarea name="message"></textarea>
      <button>送信</button>
    </form>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
  }
}
</script>

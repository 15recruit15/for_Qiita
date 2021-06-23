<template> 
  <b-container> 
    <b-col offset-md="1" md="10" class="mt-3">
      <h3 class = "form-title text-center">ユーザー情報変更</h3>
      <Notification :message="error" v-if="error" class="mb-4 pb-3" />

      <b-form @submit.prevent="update">
        <b-form-group label="名前:">
          <b-form-input placeholder="Enter your nickname" required v-model="name" type="text"></b-form-input>
        </b-form-group>
        <b-form-group label="メールアドレス:">
          <b-form-input placeholder="Enter email" required v-model="email" type="email"></b-form-input>
        </b-form-group>
        <b-form-group label="パスワード:">
          <b-form-input placeholder="Enter password" required v-model="password" type="password"></b-form-input>
        </b-form-group>
        <b-form-group label="パスワード確認用:">
          <b-form-input placeholder="password confirmation" required v-model="password_confirmation" type="password"></b-form-input>
        </b-form-group>
        <b-button block type="submit" variant="primary">Submit</b-button>
      </b-form>
    </b-col>
  </b-container>
</template>

<script>

export default{
  middleware: 'auth',
  data: function () {
    return {
        name: '',
        email: '',
        password: '',
        password_confirmation: '',
        error: null
    }
  },
  methods: {
    async update() {
      try{
        await this.$axios.$put('/api/auth',{
            name: this.name,
            email: this.email,
            password: this.password,
            password_confirmation: this.password_confirmation
        })
        this.$router.push('/')
      }catch(e){
        this.error = e.response.data.errors.full_messages
      }
    }
  }
}
</script>

<style></style>
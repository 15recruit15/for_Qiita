<template> 
    <b-container> 
      <b-col offset-md="1" md="10" class="mt-3">
        <h3 class = "text-center">ログイン</h3>

          <Notification :message="error" v-if="error" class="mb-4 pb-3" />

          <b-form @submit.prevent="login">
            <b-form-group label="メールアドレス:">
              <b-form-input placeholder="Enter email" required v-model="email" type="email"></b-form-input>
            </b-form-group>
            <b-form-group label="パスワード:">
              <b-form-input placeholder="Enter password" required v-model="password" type="password"></b-form-input>
            </b-form-group>
            <b-button block type="submit" variant="primary">送信</b-button>
          </b-form>
      </b-col>
    </b-container>
</template>

<script>
  export default {
    data: function () {
      return {
        email: '',
        password: '',
        error: null,
      }
    },
    methods: {
      async login() {
          await this.$auth.loginWith('local', {
            data: {
              password: this.password,
              email: this.email
            }
          })
          .then(
            (res) => {
            },
            (error) => {
              this.error = error.response.data.errors
            }
          )
      }
    }
  }
</script>

<style></style>
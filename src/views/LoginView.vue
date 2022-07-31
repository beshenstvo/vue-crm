<template>
    <form class="card auth-card" @submit.prevent="submit">
        <div class="card-content">
            <span class="card-title">Домашняя бухгалтерия</span>
            <div class="input-field">
            <input
                id="email"
                type="text"
                v-model.trim="email"
                @blur="v$.email.$touch"
                :class="{validate: !v$.email.$error, invalid: v$.email.$error}"
            >
            <label for="email">Email</label>
            <div class="input-errors" v-if="v$.email.$error">
              <small class="helper-text invalid">Email field has an error</small>
            </div>
            </div>
            <div class="input-field">
            <input
                id="password"
                type="password"
                v-model="password"
                @blur="v$.password.$touch"
                :class="{'validate': !v$.password.$error, invalid: v$.password.$error}"
            >
            <label for="password">Пароль</label>
            <div class="input-errors" v-if="v$.password.$error">
              <small class="helper-text invalid">Password field has an error</small>
            </div>
            </div>
        </div>
        <div class="card-action">
            <div>
            <button
                class="btn waves-effect waves-light auth-submit"
                type="submit"
            >
                Войти
                <i class="material-icons right">send</i>
            </button>
            </div>

            <p class="center">
            Нет аккаунта?
            <router-link to="/register">Зарегистрироваться</router-link>
            </p>
        </div>
    </form>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'
import { msg } from '../utils/messages'
// import M from 'materialize-css'

export default {
  setup () {
    return { v$: useVuelidate() }
  },
  data () {
    return {
      email: '',
      password: ''
    }
  },
  mounted () {
    if ((this.$route.query.message != null) && (msg[this.$route.query.message])) {
      this.$message(msg[this.$route.query.message])
    }
  },
  methods: {
    submit () {
      if (this.v$.$invalid) {
        this.v$.$touch()
        return alert('Неверно заполнены поля!')
      } else {
        // отправка данных на сервер
        this.$router.push('/')
      }
    }
  },
  validations () {
    return {
      email: { required, email },
      password: { required, minLength: minLength(6) }
    }
  }
}
</script>

<style scoped>
  .mytoast {
    background-color: aqua !important;
  }
</style>

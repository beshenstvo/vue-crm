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
        <div class="input-field">
        <input
            id="name"
            type="text"
            v-model="name"
            @blur="v$.name.$touch"
            :class="{'validate': !v$.name.$error, invalid: v$.name.$error}"
        >
        <label for="name">Имя</label>
        <div class="input-errors" v-if="v$.name.$error">
            <small class="helper-text invalid">Поле не должно быть пустым</small>
        </div>
        </div>
        <p>
        <label>
            <input type="checkbox"  v-model="checkbox"/>
            <span>С правилами согласен</span>
        </label>
        </p>
    </div>
    <div class="card-action">
        <div>
        <button
            class="btn waves-effect waves-light auth-submit"
            type="submit"
        >
            Зарегистрироваться
            <i class="material-icons right">send</i>
        </button>
        </div>

        <p class="center">
        Уже есть аккаунт?
        <router-link to="login">Войти!</router-link>
        </p>
    </div>
    </form>
</template>

<script>
import useVuelidate from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'

export default {
  setup () {
    return { v$: useVuelidate() }
  },
  data () {
    return {
      email: '',
      password: '',
      name: '',
      checkbox: false
    }
  },
  methods: {
    submit () {
      console.log(this.v$.$invalid)
      this.v$.$touch()
      if (this.v$.$invalid && this.checkbox) {
        alert('Неверно заполнены поля!')
        return 0
      } else if (this.checkbox) {
        // отправка данных на сервер
        const formData = {
          email: this.email,
          password: this.password,
          name: this.name
        }
        console.log(formData)
        this.$router.push('/')
      } else {
        return alert('Необходимо соглашение с правилами')
      }
    }
  },
  validations () {
    return {
      email: { required, email },
      password: { required, minLength: minLength(6) },
      name: { required, minLength: minLength(2) },
      checkbox: { checked: v => v }
    }
  }
}
</script>

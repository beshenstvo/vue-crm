<template>
    <nav class="navbar orange lighten-1">
    <div class="nav-wrapper">
        <div class="navbar-left">
        <a href="#" @click.prevent="$emit('clickInNavbar')">
            <i class="material-icons black-text">dehaze</i>
        </a>
        <span class="black-text">{{ date }}</span>
        </div>

        <ul class="right hide-on-small-and-down">
        <li>
            <a
                class="dropdown-trigger black-text"
                href="#"
                data-target="dropdown"
                ref="dropdown"
            >
            USER NAME
            <i class="material-icons right">arrow_drop_down</i>
            </a>

            <ul id='dropdown' class='dropdown-content'>
            <li>
                <router-link to="profile" class="black-text"><i class="material-icons">account_circle</i>Профиль</router-link>
            </li>
            <li class="divider" tabindex="-1"></li>
            <li>
                <a href="#" class="black-text" @click.prevent="logout()">
                <i class="material-icons">assignment_return</i>Выйти
                </a>
            </li>
            </ul>
        </li>
        </ul>
    </div>
    </nav>
</template>

<script>
import M from 'materialize-css'
export default {
  data: () => ({
    interval: '',
    dropdown: '',
    date: new Date().toLocaleString()
  }),
  mounted () {
    this.dropdown = M.Dropdown.init(this.$refs.dropdown, {
      inDuration: 400
    })
    this.interval = setInterval(() => {
      this.date = new Date().toLocaleString()
    }, 1000)
  },
  methods: {
    logout () {
      console.log('logout')
      this.$router.push('/login?message=logout')
    }
  },
  beforeUnmount () {
    clearInterval(this.interval)
    console.log('destroy')
  }
}
</script>

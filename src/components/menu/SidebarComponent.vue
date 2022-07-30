<template>
  <ul class="sidenav app-sidenav" :class="{'open': value}">
       <router-link v-for="link in links" :key="link.path" :to='link.path'>
          <li :class="{'myactive': link.path===this.$router.currentRoute._value.name}"><a class="wave-effects pointer">{{ link.title }}</a></li>
      </router-link>
  </ul>
</template>

<script>
export default {
  props: ['value'],
  data: () => ({
    activeEl: 0,
    links: [
      { title: 'Счет', path: 'home' },
      { title: 'История', path: 'history' },
      { title: 'Планирование', path: 'planning' },
      { title: 'Новая запись', path: 'record' },
      { title: 'Категории', path: 'categories' }
    ]
  }),
  mounted () {
    console.log(this.$router.currentRoute._value.name)
  }
}
</script>

<style scoped>
  .myactive {
    background-color: rgba(155, 155, 155, 0.339);
  }
</style>

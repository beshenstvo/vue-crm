<template>
   <div class="app-main-layout">

      <Navbar @clickInNavbar="isOpen = !isOpen"/>

      <Sidebar :value="isOpen"/>

      <main class="app-content" :class="{full: !isOpen}">
      <div class="app-page">
         <router-view/>
      </div>
      </main>

      <div class="fixed-action-btn">
         <router-link class="btn-floating btn-large blue" to="record">
            <i class="large material-icons">add</i>
         </router-link>
      </div>
   </div>
</template>

<script>
import Navbar from '@/components/menu/NavbarComponent.vue'
import Sidebar from '@/components/menu/SidebarComponent.vue'

export default {
  data () {
    return {
      isOpen: true
    }
  },
  components: {
    Navbar, Sidebar
  }
}
</script>

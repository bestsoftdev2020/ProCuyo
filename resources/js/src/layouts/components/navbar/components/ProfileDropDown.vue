<template>
  <div class="the-navbar__user-meta flex items-center" v-if="activeUserInfo.displayName">

    <div class="text-right leading-tight hidden sm:block">
      <p class="font-semibold">{{ activeUserInfo.displayName }}</p>
      <small>{{ activeUserInfo.userName }}</small>
    </div>

    <vs-dropdown vs-custom-content vs-trigger-click class="cursor-pointer">

      <div class="con-img ml-3">
        <img v-if="activeUserInfo.photoURL" key="onlineImg" :src="activeUserInfo.photoURL" alt="user-img" width="40" height="40" class="rounded-full shadow-md cursor-pointer block" />
      </div>

      <vs-dropdown-menu class="vx-navbar-dropdown">
        <ul style="min-width: 9rem">
          <li
            class="flex py-2 px-4 cursor-pointer hover:bg-primary hover:text-white"
            @click="logout">
            <feather-icon icon="LogOutIcon" svgClasses="w-4 h-4" />
            <span class="ml-2" style="width:100px;">Cerrar Sesion</span>
          </li>
        </ul>
      </vs-dropdown-menu>
    </vs-dropdown>
  </div>
</template>

<script>

export default {
  data() {
    return {

    }
  },
  computed: {
    activeUserInfo() {
      return this.$store.state.AppActiveUser
    }
  },
  methods: {
    logout() {
        // If JWT login
        if(localStorage.getItem("accessToken")) {
          localStorage.removeItem("accessToken")
          this.$router.push('/login').catch(() => {})
        }

        // Change role on logout. Same value as initialRole of acj.js
        this.$acl.change('admin')
        localStorage.removeItem('userInfo')

        // This is just for demo Purpose. If user clicks on logout -> redirect
        this.$router.push('/login').catch(() => {})
    },
  }
}
</script>

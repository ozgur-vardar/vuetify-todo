<template>
  <v-app id="inspire">
    <v-navigation-drawer
        app
        v-model="drawer"
        :mobile-breakpoint="750"
    >
      <v-img
        class="pa-4 pt-6"
        height="150"
        src="mountains.png"
        gradient="to top right, rgba(55,236,186,.7), rgba(25,32,72,.7)"
      >
        <v-avatar size="60" class="mb-2">
          <img
            src="profile.png"
            alt="profile"
          >
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          profile
        </div>
        <div class="white--text text-subtitle-2">profile123</div>
      </v-img>

      <v-list
          dense
          nav
      >
        <v-list-item
            v-for="item in items"
            :key="item.title"
            :to="item.to"
            link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
        app
        color="primary"
        dark
        prominent
        height="150"
        src="mountains.png"
    >
      <template v-slot:img="{ props }">
        <v-img
            v-bind="props"
            gradient="to top right, rgba(55,236,186,.7), rgba(25,32,72,.7)"
        ></v-img>
      </template>

      <v-container class="header-container">
        <v-row>
          <v-app-bar-nav-icon
              @click="drawer = !drawer"
          ></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search/>
        </v-row>
        <v-row>
          <v-app-bar-title>{{ $store.state.appTitle }}</v-app-bar-title>
        </v-row>
        <v-row>
          <live-date-time/>
        </v-row>
      </v-container>


    </v-app-bar>

    <v-main>
      <router-view/>
      <snackbar/>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Todo', icon: 'mdi-format-list-checks', to: '/'},
      { title: 'About', icon: 'mdi-help-box', to: '/about'},
    ],
  }),
  components: {
    'snackbar': require('@/components/Shared/SnackBar').default,
    'search': require('@/components/Tools/Search').default,
    'live-date-time': require('@/components/Tools/LiveDateTime').default,
  },
  mounted() {
    this.$store.dispatch('getTasks')
  }
}
</script>
<style lang="sass">
  .header-container
    max-width: none !important
</style>
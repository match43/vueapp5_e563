<!-- App.vue -->
<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
    >
      <lang-selector />
      <template v-slot:prepend>
        <v-list-item two-line>
        
          <v-list-item-avatar>
            <img src="https://randomuser.me/api/portraits/women/81.jpg">
          </v-list-item-avatar>
          
       
          <v-list-item-content>
            <v-list-item-title>Jane Smith</v-list-item-title>
            <nuxt-link to="login">
            <v-list-item-subtitle>Login</v-list-item-subtitle></nuxt-link>
          </v-list-item-content>
        </v-list-item>
      </template>
      <v-divider />
      <v-list dense>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          @click=""
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
    <div>
      <v-app-bar color="pink accent-2" >
        <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
        <v-toolbar-title>Chaiyaphum Technical College</v-toolbar-title>
        <v-spacer />
        <nuxt-link to="/">
        <v-btn icon>
          <v-icon large>home</v-icon>
        </v-btn>
        </nuxt-link>
        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
        <v-menu
          left
          bottom
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              icon
              v-bind="attrs"
              v-on="on"
            >
              <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
          </template>
          <v-list>
            <v-list-item
              v-for="n in 5"
              :key="n"
              @click="() => {}"
            >
              <v-list-item-title>Option {{ n }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-app-bar>
    </div>
    <!-- Sizes your content based upon application components -->
    <v-main>
      <!-- Provides the application the proper gutter -->
      <v-content>
        <nuxt />
      </v-content>
    </v-main>
    <v-footer app>
      <!-- -->
    </v-footer>
  </v-app>
</template>
<script>
import LangSelector from '~/components/lang-selector.vue'
export default {
  components: {
    LangSelector,
  },
  data () {
    return {
      items: [
        { title: 'Home', icon: 'mdi-home-city' },
        { title: 'My Account', icon: 'mdi-account' },
        { title: 'Users', icon: 'mdi-account-group-outline' },
      ],
    }
  },
  computed: {
    drawer: {
      get() {
        return this.$store.state.drawer
      },
      set(v) {
        this.$store.commit('setDrawer', v)
      },
    },
  }, // computed
  watch: {
    '$store.state.lang'() {
      this.$i18n.locale = this.$store.state.lang
    },
  }, // watch
}
</script>
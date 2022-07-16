<template>
  <v-app id="booxplorer">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <nav role="navigation">
          <v-list>
              <v-list-item-group>
                  <router-link to="/" class="router-link">
                      <v-list-item>
                          <v-list-item-icon>
                              <v-icon>mdi-home</v-icon>
                          </v-list-item-icon>
                          <v-list-item-content>
                              <v-list-item-title>Početna</v-list-item-title>
                          </v-list-item-content>
                      </v-list-item>
                  </router-link>
                  
                  <router-link to="/explore" class="router-link">
                      <v-list-item>
                          <v-list-item-icon>
                              <v-icon>mdi-star-three-points-outline</v-icon>
                          </v-list-item-icon>
                          <v-list-item-content>
                              <v-list-item-title>Istraži</v-list-item-title>
                          </v-list-item-content>
                      </v-list-item>
                  </router-link>
                  
                  <router-link to="/about" class="router-link">
                      <v-list-item>
                          <v-list-item-icon>
                              <v-icon>mdi-information-variant</v-icon>
                          </v-list-item-icon>
                          <v-list-item-content>
                              <v-list-item-title>O projektu</v-list-item-title>
                          </v-list-item-content>
                      </v-list-item>
                  </router-link>

              </v-list-item-group>
          </v-list>
      </nav>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Book-explorer</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <v-container>
        <router-view />
      </v-container>
    </v-main>

    <v-footer>
      <Footer />
    </v-footer>
  </v-app>
</template>

<script>
import Footer from '@/components/Footer.vue'

export default {
  name: 'App',

  components: {
    Footer
  },

  data: () => ({
    drawer: null
  }),
};
</script>

<style scoped>
.router-link {
    text-decoration: none;
}
</style>
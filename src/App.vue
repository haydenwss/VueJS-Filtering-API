<template class="page--background"> 
<!-- *------* -->
<!-- APP BAR  -->

  <v-app id="inspire">
    <!-- *-------------------------* -->
    <!-- LEFT SIDE NAVIGATION DRAWER -->
    <v-navigation-drawer 
      v-model="drawer"
      app
      color="#7d90f6"
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title">
              Wizard-API
          </v-list-item-title>

          <v-list-item-subtitle>
              <small>search your favourite characters</small>
          </v-list-item-subtitle>
        </v-list-item-content>

        <v-avatar size="62" >
          <img src="images/nevil.png" alt="Nev">
        </v-avatar>
      </v-list-item>

      <v-divider></v-divider>

      <!-- NAV DRAWER LINKS LOOP -->
      <!-- *-------------------* -->

      <v-list nav>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon color="white">{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title ><p>{{ item.title }}</p></v-list-item-title>
          </v-list-item-content>

        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      dark
      prominent
      class="nav--image"
      src="https://wallpaper.dog/large/964111.png"
    >
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <h2>Wizard API</h2>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>mdi-weather-lightning</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <!-- ALL PAGE ROUTING HERE => handling can be found in => router/index.js -->
      <!-- *------------------------------------------------------------------* -->
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({ 
      drawer: null,
      items: [
          { title: 'Replay Animation', icon: 'mdi-draw', to: '/' },
          { title: 'Search Wizards', icon: 'mdi-text-search', to: '/home' },
        ],
      }),
  }
</script>

<template>
    <nav>

        <v-app-bar flat app>
            <v-app-bar-nav-icon class="grey--text" @click="drawer = !drawer"></v-app-bar-nav-icon>
            <v-toolbar-title class="text-uppercase grey--text" >
                <span>AdminPanel</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>

            <!-- dropdown menu -->

            <v-menu offset-y>
                <template v-slot:activator="{ on, attrs }">
                    <v-btn depressed color="grey-lighten-2" v-bind="attrs" v-on="on">
                        <v-icon left class="grey--text">mdi-arrow-down-drop-circle-outline</v-icon>
                        <span class="grey--text">Menu</span>
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
                        <v-list-item-title>{{link.text}}</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

            <v-btn text color="grey" @click="logout">
                <span>Sign Out</span>
                 <v-icon right>mdi-logout-variant</v-icon>
            </v-btn>
        </v-app-bar>

        
        <v-navigation-drawer dark app v-model="drawer" >

            <v-layout column align-center>
                <v-flex class="mt-5">
                    <v-avatar size="100">
                        <img src="../assets/Avatar.png" alt="">
                    </v-avatar>
                    <p  style="text-align:center" class="white--text mt-1 subheading align-center">{{userName}}</p>
                </v-flex>
            </v-layout>
            <v-divider></v-divider>
            <v-list>
                <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
                    <v-list-item-action>
                        <v-icon class="white--text">{{link.icon}}</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title class="white--text">
                            {{link.text }}
                        </v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
    </nav>
</template>

<script>
export default {
  data: () => ({ 
    drawer: false,
    links: [
        {icon: 'mdi-view-dashboard', text: 'Dashboard', route: '/'},
        {icon: 'mdi-folder', text: 'About', route: '/about'},
        {icon: 'mdi-information-outline', text: 'Info', route: '/info'},
    ],
    userName : ''
  }),
  methods: {
    async logout() {
      localStorage.clear();
      this.$router.push("/login");
    },
  },
  created(){
    // console.log(localStorage.getItem('accessToken'));
    this.userName = localStorage.getItem('userName');
  }

}
</script>

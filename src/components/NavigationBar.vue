<template>
  <v-navigation-drawer 
      color="green"
      dark
      expand-on-hover
      hide-overlay
      permanent  
      right 
      app
    >
      <v-list
        nav
        shape
        dense
      >
        <v-list-item two-line>
          <v-list-item-avatar>
            <img :src="avatar">
          </v-list-item-avatar>

          <v-list-item-content class="text-left">
            <v-list-item-title class="font-weight-black">
              {{ userName }}
            </v-list-item-title>
            <v-list-item-subtitle>
              {{  userEmail }}
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>    

        <v-divider class="my-3"></v-divider>

        <v-list-item link to="/">
          <v-list-item-icon>
            <v-icon>mdi-home-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">
              MAIN
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link :to="userLink">
          <v-list-item-icon>
            <v-icon>mdi-account-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">
              ACCOUNT
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link to="/users">
          <v-list-item-icon>
            <v-icon>mdi-account-multiple-plus-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">
              FIND FRIENDS
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="$emit('logout')">
          <v-list-item-icon>
            <v-icon>mdi-arrow-expand-right</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">
              LOG OUT
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

      </v-list>
    </v-navigation-drawer>
</template>

<script>
export default {
  name: "NavigationBar",
  props: ['userLink', 'userName', 'userEmail', 'avatar'],
}
</script>
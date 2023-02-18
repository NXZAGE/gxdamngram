<template>
  <div>
    <v-row 
    v-for="(user) of this.users" :key="user.id"
    >
      <v-list-item 
        two-line
        link :to="getUserLink(user.id)"
      >
        <v-list-item-avatar>
          <img :src="user.photo">
        </v-list-item-avatar>

        <v-list-item-content class="text-left">
          <v-list-item-title class="font-weight-black">
            {{ user.name }}
          </v-list-item-title>
          <v-list-item-subtitle>
            {{ user.email }}
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "FindFriends",
  data() {
    return {
      users: [],
      user: {
        id: -1,
        name: "Anonym",
        email: "Anonim@example.some",
        image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7SRfJKEFNq48W0XyVM15kteOBUObrU1GnxDHH0wCNNg&s",
      }
    };
  },
  methods: {
    prepareUsers() {
      let api = "https://api.npoint.io/7b537035221a819d5d7c";
      
      this.axios.get(api).then((response) => {
        this.users = response.data.users;
      })
    },
    getUserLink(id) {
      return "/user/" + id;
    }
  },
  mounted() {
    this.prepareUsers();
  }
};
</script>
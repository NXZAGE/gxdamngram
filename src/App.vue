<template>
  <v-app>
    <NavigationBar :userName="user.name" :userEmail="user.email" :avatar="user.image" :userLink="accountLink"/>

    <v-main class="px-12 py-3">
      <v-container fluid>
        <router-view @authenticated="authentication" @logout="logout"/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import NavigationBar from "./components/NavigationBar.vue"

export default {
  name: "App",
  components: {
    NavigationBar
  },
  data() {
    return {
      user: {
        id: -1,
        name: "Anonim",
        email: "Anonim",
        phone: "???",
        city: "???",
        company: "???",
        image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7SRfJKEFNq48W0XyVM15kteOBUObrU1GnxDHH0wCNNg&s"
      },
    }
  },
  computed: {
    accountLink: function(){
      if (this.user.id == -1){
        return "/login";
      }
      return "/user/" + this.user.id
    }  
  },
  methods: {
    authentication(id) {
      this.user.id = Number(id);
      this.getUser();
      console.log(this.user.name);
      this.$router.push('/user/' + id);
    },
    logout() {
      console.log("logged out");
      this.user.id = -1;
      this.user.name = "Anonim";
      this.user.email = "Anonim"; 
      this.user.phone = "???";
      this.user.city = "???";
      this.user.company = "???";
      this.user.image = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7SRfJKEFNq48W0XyVM15kteOBUObrU1GnxDHH0wCNNg&s";
    },
    getUser() {
      let api = "https://api.npoint.io/7b537035221a819d5d7c";
      
      this.axios.get(api).then((response) => {
        let currentUserID = this.user.id;
        let allUsers = response.data.users;
        console.log(allUsers);
        for (let i in allUsers) {
          let user = allUsers[i];
          if (user.id == currentUserID) {
            console.log(user.name);
            this.user.id = user.id;
            this.user.name = user.name;
            this.user.phone = user.phone;
            this.user.email = user.email;
            this.user.city = user.city;
            this.user.company = user.company;
            this.user.image = user.photo;
            console.log(this.user.name);
            break;
          }
        }
      })
    }
  }
};
</script>

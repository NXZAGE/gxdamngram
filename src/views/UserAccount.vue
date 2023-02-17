<template>
  <div>
    <v-row class="text-left">
      <v-col cols="10">
        <h1 class="green--text text--darken-2">
          <v-icon large color="green darken-2">mdi-account-outline</v-icon>
          {{ user.name }}
        </h1>
      </v-col>
    </v-row>
    <v-row class="text-left">
      <v-col cols="2">
        <v-img :src="user.image" height="20px" width="20px" covered/>
      </v-col>
      <v-col cols="8" class="text-left">
        <p>
          ID: {{ user.id }}
        </p>
        <p>
          E-mail: <a :href="getEmailLink(user.email)">{{ user.email }}</a>
        </p>
        <p>
          Телефон: {{ user.phone }}
        </p>
        <p>
          Город: {{ user.city }}
        </p>
        <p>
          Место работы: {{  user.company }}
        </p>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="10" v-for="(post, i) in posts" :key="i">
        <UserPost/>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import UserPost from "../components/UserPost.vue"

  export default {
    name: "UserAccount",
    components: {
      UserPost
    },
    data() { 
      return {
        user: {
          id: -1,
          name: "",
          email: "",
          phone: "",
          city: "",
          company: "",
          image: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR7SRfJKEFNq48W0XyVM15kteOBUObrU1GnxDHH0wCNNg&s"
        },
        posts: []
      }
    },
    methods: {
      getEmailLink(email) {
        return "https://malta:" + email;
      },
      getUserData() {
        let api = "https://api.npoint.io/7b537035221a819d5d7c";
        this.axios.get(api).then((response) => {
          let users = response.data.users;
          let currentUserID = Number(this.$route.params.id);

          for (let i in users){
            let user = users[i];
            if (user.id == currentUserID){
              this.user.id = currentUserID;
              this.user.name = user.name;
              this.user.phone = user.phone;
              this.user.email = user.email;
              this.user.city = user.city;
              this.user.company = user.company;
              this.user.image = user.photo;
              return;
            }
          }
          console.log("There is no users with this id!");
        })
      },
      getUserPosts() {
        let api = "https://api.npoint.io/7b537035221a819d5d7c";
        this.axios.get(api).then((response) => {
          let allPosts = response.data.posts;
          for (let i in allPosts){
            let post = allPosts[i];
            if (post.author_id == this.user.id)
            {
              this.posts.push(post);
            }
          }
        })
      }
    },
    mounted() {
      console.log("mounted" + this.id);
      this.getUserData();
      this.getUserPosts();
    }
  };
</script>
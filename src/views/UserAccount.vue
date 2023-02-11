<template>
  <div>
    <h1>{{ id }}</h1>
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
        <img src="https://randomuser.me/api/portraits/men/7.jpg" style="max-width: 100%">
      </v-col>
      <v-col cols="8" class="text-left">
        <p>
          Веб-сайт: <a :href="getWebsiteLink(user.website)" target="_blank">{{ user.website }}</a>
        </p>
        <p>
          E-mail: <a :href="getEmailLink(user.email)">{{ user.email }}</a>
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
      <v-col cols="10">
        <UserPost/>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="10">
        <UserPost/>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="10">
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
          name: "Ivan Ivanov",
          website: "github.com",
          email: "example@gmail.com",
          city: "Los Angeles",
          company: "Worm home"
        },
        id: this.$route.params.id,
        posts: []
      }
    },
    methods: {
      getEmailLink(email) {
        return "https://malta:" + email;
      },
      getWebsiteLink(website) {
        return "https://" + website;
      },
      getUserData() {
        let api = "https://api.npoint.io/949f260cfed82dbe321f";
        this.axios.get(api).then((response) => {
          let allPosts = response.data.posts;
          for (let i in allPosts){
            let post = allPosts[i];
            if (post.author_is == this.id)
            {
              this.posts += post; 
            }
          }
          console.log(this.posts)
        })
      }
    },
    watch: {
      $route() {
        console.log("vizvano")
        //this.getUserData();
      }
    }
  };
</script>
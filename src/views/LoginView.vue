<template>
  <div class="d-flex justify-center">
    <v-card width="600px" class="mt-12 pa-10" outlined>
      <v-card-title>
        Войдите в аккаунт
      </v-card-title>

      <v-text-field label="Введите логин" v-model="login" outlined></v-text-field>

      <v-text-field label="Введите пароль" v-model="password" outlined></v-text-field>

      <v-btn outlined @click="authenticate">
        Войти
      </v-btn>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      password: "",
      login: "",
    }
  },
  methods: {
    authenticate() {
      let api = "https://api.npoint.io/7b537035221a819d5d7c";
      this.axios.get(api).then((response) => {
        let users = response.data.users;
        for(let i in users){
          let user = users[i];
          if (user.login == this.login && user.password == this.password){
            console.log("authenticated");
            this.$emit('authenticated', user.id);
            return;
          }
        }
        alert("not founded user");
      })
      // let json_string;
      // let dbFile = new File([json_string], "/src/assets/db.json");
      // let reader = new FileReader();
      // console.log(dbFile)
      // console.log(json_string)
      // let db = JSON.parse(reader.readAsText(dbFile));
      // let users = db["users"];
      // console.log("json string is");
      // console.log(json_string);
      // console.log("db is")
      // console.log(db)
      // console.log("users is")
      // console.log(users)
      // for (let user in users){
      //   console.log(user["login"]);
      // }
    }
  }
}
</script>
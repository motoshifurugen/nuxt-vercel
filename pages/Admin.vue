<template>
  <v-app>
    <Header />
    <v-container>
      <div class="admin-body">
        <h1>結果入力画面</h1>
        <v-form
          ref="form"
          v-model="valid"
          lazy-validation
        >

          <v-select
            v-model="greatTeam"
            :items="entryTeams"
            :rules="[v => !!v || '最優秀賞が登録されていいません。']"
            attach
            chips
            label="最優秀賞"
          ></v-select>

          <v-select
            v-model="effortTeams"
            :items="entryTeams"
            attach
            chips
            label="努力賞"
            multiple
          ></v-select>

          <v-btn
            color="error"
            class="mr-4 admin-btn reset"
            @click="reset"
            large
          >
            リセット
          </v-btn>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4 admin-btn submit"
            @click="submit"
            large
          >
            登録
          </v-btn>

          <v-overlay :value="overlay">
            <v-progress-circular
              indeterminate
              size="64"
            ></v-progress-circular>
          </v-overlay>

        </v-form>
      </div>
    </v-container>
  </v-app>
</template>


<style scoped>
.admin-body {
  margin: 100px 0;
  padding-bottom: 100px;
}
.admin-btn {
  margin: 2em 0;
  font-size: 1em;
}
</style>


<script>
import Header from "../components/Header.vue"

export default {
  components: { Header },
  data: () => ({
    valid: true,
    greatTeam: [],
    effortTeams: [],
    entryTeams: [
      'JavaScript',
      'Python',
      'TypeScript',
      'Go',
      'Swift',
      'HTML, CSS',
      'C++',
      'Java',
      'Ruby',
      'C#',
      'PHP',
      'Kotlin',
      'その他',
    ],
    overlay: false,
  }),
  methods: {
    submit () {
      if (this.$refs.form.validate()) {
        this.overlay = true
        location.reload();
      }
    },
    reset () {
      this.$refs.form.reset()
    },
  },
}
</script>
<template>
  <v-app>
    <Header />
    <v-container>
      <div class="entry-body">
        <h1>チーム登録画面</h1>
        <v-form
          ref="form"
          v-model="valid"
          lazy-validation
        >
          <v-text-field
            v-model="name"
            :counter="20"
            :rules="nameRules"
            label="チーム名"
            required
          ></v-text-field>

          <v-text-field
            v-model="portfolio"
            :rules="portfolioRules"
            label="制作したもの"
            required
          ></v-text-field>

          <!-- <v-select
            v-model="progLang"
            :items="languages"
            attach
            chips
            label="使用言語"
            multiple
          ></v-select>

          <v-select
            v-model="progTech"
            :items="technologies"
            attach
            chips
            label="使用技術"
            multiple
          ></v-select> -->

          <v-btn
            color="error"
            class="mr-4 entry-btn reset"
            @click="reset"
            large
          >
            リセット
          </v-btn>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4 entry-btn submit"
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
.entry-body {
  margin: 100px 0;
  padding-bottom: 100px;
}
.entry-btn {
  margin: 2em 0;
  font-size: 1em;
}
</style>


<script>
import Header from "../components/Header.vue"
import axios from "axios"

export default {
  components: { Header },
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'チーム名を入力してください。',
      v => (v && v.length <= 20) || '20文字以内で入力してください。',
    ],
    portfolio: '',
    portfolioRules: [
      v => !!v || '制作したものを教えてください。',
    ],
    progLang: [],
    progTech: [],
    languages: [
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
    technologies: [
      'Firebase',
      'React',
      'Vue.js',
      'MySQL',
      'Flask',
      'jQuery',
      'PostgreSQL',
      'TensorFlow',
      'Heroku',
      'Next.js',
      'Flutter',
      'SQLite',
      'Keras',
      'Django',
      'Ruby on Rails',
      'Xamarin',
      'Angular',
    ],
    overlay: false,
  }),
  methods: {
    submit () {
      if (this.$refs.form.validate()) {
        const data = {
          name: this.name,
          work: this.portfolio
        }
        axios
          .post("/api/teams/", data)
          .then(response => {
            this.overlay = true
            alert('登録しました')
            location.reload()
          });
      }
    },
    reset () {
      this.$refs.form.reset()
    },
  },
}
</script>
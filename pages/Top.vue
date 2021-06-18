<template>
    <v-app>
        <div class="container">
            <div>
          <logo />
          <h1 class="app-title" style="color:#1B5E20;">
            ハッカソン・ダービー
          </h1>
          <h2 class="app-subtitle">
            created by charengeable.
          </h2>
          <div class="buttons">
            <v-btn
              class="btn vote"
              to="/entry"
              color="success"
              x-large
            >
              登録する
            </v-btn>
            <v-btn
              class="btn vote"
              to="#"
              color="amber darken-2"
              x-large
              dark
            >
              ランキング
            </v-btn>
            <v-btn
              class="btn vote"
              to="/vote"
              color="primary"
              x-large
            >
              投票する
            </v-btn>
          </div>
            </div>
        </div>
    </v-app>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.app-title {
  font-size: 5em;
}
.app-subtitle {
	font-size: 2em;
}
.buttons {
	margin: 2em 0;
}
.btn {
  font-size: 1.5em;
  margin: 0 1em;
}
</style>

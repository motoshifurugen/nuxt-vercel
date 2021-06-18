<template>
  <v-app>
    <Header />
    <div class="entry-body">
    </div>
  </v-app>
</template>


<style scoped>
.top-btn {
  font-size: 1.25em;
}
</style>


<script>
import Header from "../components/Header.vue"

export default {
  components: { Header },
  data: () => ({
  }),
}
</script>
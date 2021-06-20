<template>
　<v-app>
    <Header />
    <div class="ranking-body">
    <v-row justify="center">
      <v-col cols="6">
        <v-card>
          <v-card-title>
            ランキングページ
          </v-card-title>
        </v-card>
      </v-col>
    </v-row>

<v-row justify="center">
      <v-col cols="3">
        <v-btn
          v-for="number in numbers"
          :key="number.id"
          class="box-inner-btn ranking-button"
          v-bind:color="number.color"
          dark
        >
        <div class="name">
          {{ number.title }}
        </div>
        </v-btn>
      </v-col>
      <v-col cols="6" >
        <v-btn
          v-for="ranking in rankings"
          :key="ranking.id"
          class="box-inner-btn ranking-button"
          color="orange darken-2"
          dark
        >
        <div class="name">
          【チーム名】{{ ranking.name }}
          【得票数】{{ ranking.points }}
        </div>
        </v-btn>
        </v-col>
    </v-row>
  <div class="text-center">
    <v-rating
      v-model="rating"
      background-color="purple lighten-3"
      color="purple"
      large
    ></v-rating>
    <v-rating
      v-model="rating"
      background-color="pink lighten-3"
      color="pink"
      large
    ></v-rating>
    <v-rating
      v-model="rating"
      background-color="orange lighten-3"
      color="orange"
      large
    ></v-rating>
    <v-rating
      v-model="rating"
      background-color="green lighten-3"
      color="green"
      large
    ></v-rating>
    <v-rating
      v-model="rating"
      background-color="red lighten-3"
      color="red"
      large
    ></v-rating>
    <v-rating
      v-model="rating"
      background-color="indigo lighten-3"
      color="indigo"
    ></v-rating>
  </div>
  </div>
  </v-app>
</template>


<style>
.title{
 text-align: center;
}
.ranking-body{
  margin: 80px;
}

.ranking-button {
 pointer-events: none;
 margin: 1em;
 width: 100%;
 padding: 2em !important;
}
.name{
  font-size: 2em;
}

</style>

<script>
import Header from "../components/Header.vue"
import axios from "axios"

export default {
  components: { Header },
  data: () => ({
  numbers: [
      {
        id: 1,
        title: '1位',
        color: 'red darken-1'
      },
      {
        id: 2,
        title: '2位',
        color: 'blue darken-1'
      },
      {
        id: 3,
        title: '3位',
        color: 'amber'
      },
  ],
　rankings: [],
  }),
  mounted () {
    axios
      .get("/api/teams/?format=json")
      .then(response => {
        this.rankings = response.data
      });
    this.rankings.sort(function(a, b) {
      if (a.points > b.points) {
        return 1;
      } else {
        return -1;
      }
    })
  },
}
</script>
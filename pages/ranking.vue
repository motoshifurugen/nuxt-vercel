<template>
　<v-app>

    <v-row justify="center">
      <v-col cols="6">
        <v-card>
          <v-card-title>　　　ーランキングページー</v-card-title>
        </v-card>
      </v-col>
    </v-row>

        <v-btn
          v-for="ranking in rankings"
          :key="ranking.id"
          class="mx-4 box-inner-btn ranking-button"
          color="orange darken-2"
          dark
          @click="addTeam(ranking.id)"
        >
          {{ ranking.name }}
          {{ ranking.point }}
        </v-btn>
    
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
      large
    ></v-rating>
  </div>
  </v-app>
</template>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.ranking-button{
 margin-bottom: 1em;

}

</style>

<script>
import Header from "../components/Header.vue"

export default {
  components: { Header },
  data: () => ({
　rankings: [
      {
        id: 1,
        name: 'チームA',
        point: 10
      },
      {
        id: 2,
        name: 'チームB',
        point: 9
      },
      {
        id: 3,
        name: 'チームC',
        point: 8
      },
      {
        id: 4,
        name: 'チームD',
        point: 7
      },
      {
        id: 5,
        name: 'チームE',
        point: 6
      },
      {
        id: 6,
        name: 'チームF',
        point: 5
      },
      {
        id: 7,
        name: 'チームG',
        point: 4
      },
      {
        id: 8,
        name: 'チームH',
        point: 3
      },
      {
        id: 9,
        name: 'チームI',
        point: 2
      },
      {
        id: 10,
        name: 'チームJ',
        point: 1
      },
      {
        id: 11,
        name: 'チームK',
        point: 0
      },
      {
        id: 12,
        name: 'チームL',
        point: 0
      },
    ],
  }),
  
}
</script>
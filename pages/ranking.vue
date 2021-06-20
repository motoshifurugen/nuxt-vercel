<template>
　<v-app>
    <Header />
    <div class="ranking-body">
    <v-row justify="center">
      <v-col cols="6">
        <v-card>
     <v-btn block>
     <div class="ranking-title">
      <v-col cols="3">
     ランキングページ
     </v-col>
     </div>
     </v-btn>
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
          {{ ranking.name }}
          {{ ranking.point }}
        </div>
        </v-btn>
        </v-col>
     
    
    </v-row>
    
  </div>
  </v-app>
</template>


<style>
.title{
 text-align: center;
 pointer-events: none;
}

.ranking-title{
  color:"orange darken-2";
  pointer-events: none;
  font-size: 1.5em;
  padding: 2em;
}

.ranking-body{
  pointer-events: none;
  margin: 80px;
}

.ranking-button{
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
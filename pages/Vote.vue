<template>
  <v-app>
    <!-- ヘッダー -->
    <v-app-bar color="success" dark app>
      <v-toolbar-title>ハッカソン・ダービー</v-toolbar-title>
    </v-app-bar>
    <!-- ヘッダー終わり -->

  <div class="vote-body">
    <v-card
      max-width="90%"
      class="mx-auto"
    >
      <div class="vote-description teal white--text">
        <h2>今回のハッカソンで賞を受賞するチームを予想して投票！</h2>
      </div>
      <v-container class="pa-1">
        <v-item-group
          multiple
          class="vote-team-card-group"
        >
          <v-row>
            <v-col
              v-for="(team, i) in teams"
              :key="i"
              cols="6"
              md="4"
              class="vote-team-card"
            >
              <v-item>
                <v-img
                  :src="`https://cdn.vuetifyjs.com/images/${team.src}`"
                  height="150"
                  class="text-right pa-2"
                  @click="addTeam(team.id);"
                >
                {{ team.name }}
                  <v-btn
                    icon
                    dark
                  >
                    <v-icon>
                      {{ (team.selected === true) ? 'mdi-heart' : 'mdi-heart-outline' }}
                    </v-icon>
                  </v-btn>
                </v-img>
              </v-item>
            </v-col>
          </v-row>
        </v-item-group>
      </v-container>
    </v-card>
  </div>

    <!-- フッター -->
    <v-footer dark app padless class="footer success">
      <v-card
      class="vote-box flex"
      flat
      tile
    >
      <v-card-text class="vote-box-text success white--text text-center">
        <strong>投票ボックス</strong>
      </v-card-text>
      <v-card-title class="vote-box-body teal">
        <v-btn
          v-for="voteTeam in voteTeams"
          :key="voteTeam.id"
          class="mx-4"
          dark
        >
          <div>
            <p>{{ voteTeam.name }}</p>
          </div>
        </v-btn>

        <v-spacer></v-spacer>

        <strong>{{ voteCount }}/5</strong>
      </v-card-title>
    </v-card>
    </v-footer>
    <!-- フッター終わり -->
  </v-app>
</template>

<style scoped>
.vote-body {
  margin: 100px 0;
  padding-bottom: 100px;
}
.vote-box {
  padding: 0 !important;
}
.vote-box-text {
  font-size: 1.5em;
}
.vote-box-body {
  font-size: 1.5em;
}
.vote-description {
  text-align: center;
  padding:1em 0;
}
.vote-team-card-group {
  margin: 2em 1em;
}
</style>

<script>
  export default {
    data: () => ({
      voteCount: 0,
      teams: [
        {
          id: 1,
          name: 'チームA',
          src: 'backgrounds/bg.jpg',
          selected: false
        },
        {
          id: 2,
          name: 'チームB',
          src: 'backgrounds/md.jpg',
          selected: false
        },
        {
          id: 3,
          name: 'チームC',
          src: 'backgrounds/bg-2.jpg',
          selected: false
        },
        {
          id: 4,
          name: 'チームD',
          src: 'backgrounds/md2.jpg',
          selected: false
        },
        {
          id: 5,
          name: 'チームE',
          src: 'backgrounds/bg.jpg',
          selected: false
        },
        {
          id: 6,
          name: 'チームF',
          src: 'backgrounds/md.jpg',
          selected: false
        },
        {
          id: 7,
          name: 'チームG',
          src: 'backgrounds/bg-2.jpg',
          selected: false
        },
        {
          id: 8,
          name: 'チームH',
          src: 'backgrounds/md2.jpg',
          selected: false
        },
        {
          id: 9,
          name: 'チームI',
          src: 'backgrounds/bg.jpg',
          selected: false
        },
        {
          id: 10,
          name: 'チームJ',
          src: 'backgrounds/md.jpg',
          selected: false
        },
        {
          id: 11,
          name: 'チームK',
          src: 'backgrounds/bg-2.jpg',
          selected: false
        },
        {
          id: 12,
          name: 'チームL',
          src: 'backgrounds/md2.jpg',
          selected: false
        },
      ],
      voteTeams: [],
    }),
    methods: {
      addTeam (teamId) {
        var selectTeams = this.teams.find((team) => team.id === teamId)
        if (this.voteTeams.find((voteTeam) => voteTeam.id === teamId) && this.voteCount > 0) {
          this.voteTeams = this.voteTeams.filter((team) => team.id !== teamId)
          this.voteCount--
          selectTeams.selected = false
        } else if (this.voteCount < 5) {
          const addTeam = this.teams.find((team) => team.id === teamId)
          this.voteTeams.push(addTeam)
          this.voteCount++
          selectTeams.selected = true
        }
      }
    }
  }
</script>
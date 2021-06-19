<template>
  <v-app>
    <Header />

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
                    :src="`https://cdn.vuetifyjs.com/images/backgrounds/bg.jpg`"
                    height="150"
                    class="text-right pa-2"
                    @click="addTeam(team.id);"
                  >
                  {{ team.name }}
                  {{ team.work }}
                  {{ team.points }}
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
    <v-footer dark app padless class="footer success" v-show="footer">
      <v-card
      class="vote-box flex"
      flat
      tile
    >
      <v-card-text class="vote-box-text success white--text text-center">
        <strong>投票ボックス {{ voteCount }}/5</strong>
      </v-card-text>
      <v-card-title class="vote-box-body teal">
        <v-btn
          v-for="voteTeam in voteTeams"
          :key="voteTeam.id"
          class="mx-4 box-inner-btn"
          color="orange darken-2"
          dark
          @click="addTeam(voteTeam.id)"
        >
          {{ voteTeam.name | truncate }}
        </v-btn>

        <v-spacer></v-spacer>

        <v-dialog
          v-model="dialog"
          persistent
          max-width="60%"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              class="confirm-btn"
              color="deep-orange"
              dark
              v-bind="attrs"
              v-on="on"
              v-show="voteBtn"
              large
            >
              決定
            </v-btn>
          </template>
          <v-card>
            <v-card-title class="text-h5">
              以下のチームに投票します
            </v-card-title>
            <v-card-text>
              <v-chip
                v-for="(voteTeam, i) in voteTeams"
                :key="i"
                class="ma-2"
                color="orange darken-2"
                outlined
              >
                {{ voteTeam.name }}
              </v-chip>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="green darken-1"
                text
                @click="dialog = false"
              >
                キャンセル
              </v-btn>
              <v-btn
                color="deep-orange darken-1"
                text
                @click="vote"
              >
                <b>投票</b>
              </v-btn>
              <v-overlay :value="overlay">
                <v-progress-circular
                  indeterminate
                  size="64"
                ></v-progress-circular>
              </v-overlay>
            </v-card-actions>
          </v-card>
        </v-dialog>
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
.vote-team-card {
  font-weight: bold;
  cursor: pointer;
}
.confirm-btn {
  font-size: 1em;
  margin: 0 16px;
}
.box-inner-btn {
  text-align: center;
  font-size: 0.75em;
  margin: 5px 0;
}
</style>


<script>
import Header from "../components/Header.vue"
import axios from 'axios'

export default {
  components: {
    Header
  },
  data: () => ({
    footer: false,
    dialog: false,
    voteBtn: false,
    overlay: false,
    voteCount: 0,
    teams: [],
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
      if (this.voteCount === 0) {
        this.footer = false
      } else {
        this.footer = true
        if (this.voteCount === 5) {
          this.voteBtn = true
        } else {
          this.voteBtn = false
        }
      }
    },
    vote () {
      for (const team in this.voteTeams) {
        team.points++
      }
        axios
          .post("/api/teams/", this.voteTeams)
          .then(response => {
            this.overlay = true
            alert('投票しました')
            location.reload()
          });
    }
  },
  filters: {
    truncate: function(value) {
      var length = 8;
      var ommision = "...";
      if (value.length <= length) {
        return value;
      }
      return value.substring(0, length) + ommision;
    }
  },
  mounted () {
    axios
      .get("/api/teams/?format=json")
      .then(response => {
        this.teams = response.data
      });
  },
}
</script>
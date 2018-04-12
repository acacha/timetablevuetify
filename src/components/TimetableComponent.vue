<template>
  <v-container grid-list-md text-xs-center>
    <v-layout row wrap>
      <v-flex xs2>
        <v-container grid-list-md text-xs-center>
          <v-layout row wrap>
            <v-flex xs12>
              <v-card dark color="primary">
                <v-card-text class="px-0">Lliçons</v-card-text>
              </v-card>
            </v-flex>
            <v-flex xs12 v-for="lesson in lessons">
              <v-card>
                <v-card-text class="px-0">{{lesson.name}}</v-card-text>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-flex>
      <v-flex xs10>
        <v-container grid-list-md text-xs-center>
          <v-layout row wrap>
            <v-flex xs2 v-for="row in rows">
              <v-card dark color="primary">
                <v-card-text class="px-0">{{ row }}</v-card-text>
              </v-card>
            </v-flex>
            <template v-for="timeslot in timeslots">
              <v-flex xs2>
                <v-card>
                  <v-card-text class="px-0">{{ timeslot }}</v-card-text>
                </v-card>
              </v-flex>
              <v-flex xs2 v-for="i in 5">
                <v-card>
                  <v-card-text class="px-0">TODO</v-card-text>
                </v-card>
              </v-flex>
            </template>
          </v-layout>
        </v-container>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

<script>
  export default {
    data () {
      return {
        rows: ['Hora', 'Dilluns', 'Dimarts', 'Dimecres', 'Dijous', 'Divendres'],
        timeslots: ['08:00', '09:00', '10:00', '11:00', '11:30', '12:30', '13:30', '14:30', '15:30', '16:30', '17:30', '18:30', '19:00', '20:00', '21:00'],
        lessons: [
          {'name': 'UF1'},
          {'name': 'UF1'},
          {'name': 'UF1'},
          {'name': 'UF1'},
          {'name': 'UF1'},
          {'name': 'UF2'},
          {'name': 'UF2'},
          {'name': 'UF3'}
        ]
      }
    }
  }
</script>

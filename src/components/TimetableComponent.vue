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
            <v-flex xs12>
              <v-card>
                <v-card-text class="px-0">Available Dropzone</v-card-text>
              </v-card>
            </v-flex>
            <v-flex xs12 v-for="lesson in availableLessons" :key="lesson.id">
              <v-card draggable="true" @dragstart="startDraggingAvailableLesson($event,lesson)">
                <v-card-text class="px-0">{{lesson.name}}</v-card-text>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-flex>
      <v-flex xs10>
        <v-container grid-list-md text-xs-center>
          <v-layout row wrap>
            <v-flex xs2>
              <v-card dark color="primary">
                <v-card-text class="px-0" >Hora</v-card-text>
              </v-card>
            </v-flex>
            <v-flex xs2 v-for="day in days" :key="day.id">
              <v-card dark color="primary">
                <v-card-text class="px-0">{{ day.name }}</v-card-text>
              </v-card>
            </v-flex>
            <template v-for="timeslot in timeslots">
              <v-flex xs2>
                <v-card>
                  <v-card-text class="px-0">{{ timeslot.start }}</v-card-text>
                </v-card>
              </v-flex>
              <v-flex xs2 v-for="day in days" :key="day.id + '' + timeslot.id ">
                <v-card>
                  <v-card-text class="px-0" @drop="dropLesson($event, day, timeslot)" @dragover="allowDrop" v-html="content(day, timeslot )"></v-card-text>
                </v-card>
              </v-flex>
            </template>
          </v-layout>
        </v-container>
      </v-flex>
    </v-layout>
    <v-form>
      <v-text-field
              label="Name"
              v-model="newLessonName"
              required
      ></v-text-field>
      <v-text-field
              label="Day Code"
              v-model="newLessonDay"
              required
      ></v-text-field>
      <v-text-field
              label="Timeslot Code"
              v-model="newLessonTimeslot"
              required
      ></v-text-field>
    </v-form>
    <v-btn color="success" @click="addLesson">Add lesson</v-btn>
  </v-container>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  [draggable] {
    -moz-user-select: none;
    -webkit-user-select: none;
    user-select: none;
    /* Required to make elements draggable in old WebKit */
    -webkit-user-drag: element;
    cursor: move;
    cursor: move;
  }
</style>

<script>
  export default {
    data () {
      return {
        timetable: [],
        newLessonName: '',
        newLessonDay: 0,
        newLessonTimeslot: 0,
        days: [
          {
            'id': 1,
            'name': 'Dilluns'
          },
          {
            'id': 2,
            'name': 'Dimarts'
          },
          {
            'id': 3,
            'name': 'Dimecres'
          },
          {
            'id': 4,
            'name': 'Dijous'
          },
          {
            'id': 5,
            'name': 'Divendres'
          }
        ],
        timeslots: [
          {
            'id': 1,
            'start': '08:00',
            'end': '09:00'
          },
          {
            'id': 2,
            'start': '09:00',
            'end': '10:00'
          },
          {
            'id': 3,
            'start': '10:00',
            'end': '11:00'
          },
          {
            'id': 4,
            'start': '11:00',
            'end': '11:30'
          },
          {
            'id': 5,
            'start': '11:30',
            'end': '12:30'
          },
          {
            'id': 6,
            'start': '12:30',
            'end': '13:30'
          },
          {
            'id': 7,
            'start': '13:30',
            'end': '14:30'
          }
        ],
        lessons: [
          {
            'id': 1,
            'name': 'UF1',
            'day': 1,
            'timeslot_id': 7
          }
        ],
        availableLessons: [
          {
            'id': 1,
            'name': 'UF1'
          },
          {
            'id': 2,
            'name': 'UF1'
          },
          {
            'id': 3,
            'name': 'UF1'
          },
          {
            'id': 4,
            'name': 'UF1'
          },
          {
            'id': 5,
            'name': 'UF1'
          },
          {
            'id': 6,
            'name': 'UF2'
          },
          {
            'id': 7,
            'name': 'UF2'
          },
          {
            'id': 8,
            'name': 'UF3'
          }
        ]
      }
    },
    methods: {
      addLesson () {
        const newLesson = {
          'name': this.newLessonName,
          'day': parseInt(this.newLessonDay),
          'timeslot_id': parseInt(this.newLessonTimeslot)
        }
//        console.log(newLesson)
        this.lessons.push(newLesson)
      },
      content (day, timeslot) {
//        console.log('Day:')
//        console.log(day.name)
//        console.log('Timeslot:')
//        console.log(timeslot.start)
//        console.log(timeslot.id)

        const lesson = this.lessons.find(function (lesson) {
          return lesson.day === day.id && lesson.timeslot_id === timeslot.id
        })
        return lesson ? lesson.name : '&nbsp;'
      },
      allowDrop (e) {
        e.preventDefault()
      },
      dropLesson (e, day, timeslot) {
//        console.log(e)
        const lesson = JSON.parse(e.dataTransfer.getData('lesson'))
//        console.log('Lesson is:', lesson)
//        console.log('Lesson name:', lesson.name)
//        console.log('Lesson id:', lesson.id)
//        console.log('Lesson By id:', this.getLessonById(lesson.id))
        // Remove lesson from available availableLessons:
        this.availableLessons.splice(this.availableLessons.indexOf(this.getLessonById(lesson.id)), 1)
//        console.log('DAY:')
//        console.log(day)
//        console.log(day.id)
//        console.log('TIMESLOT:')
//        console.log(timeslot)
//        console.log(timeslot.id)
        this.newLessonName = lesson.name
        this.newLessonDay = day.id
        this.newLessonTimeslot = timeslot.id
        this.addLesson()
      },
      getLessonById (id) {
        return this.availableLessons.find(function (lesson) {
          return lesson.id === id
        })
      },
      startDraggingAvailableLesson (e, lesson) {
//        console.log('Starting drag lesson:')
//        console.log(lesson.name)
//        console.log(lesson)
//        console.log('Event:')
//        console.log(e)
        e.dataTransfer.effectAllowed = 'move'
        e.dataTransfer.setData('lesson', JSON.stringify(lesson))
      }
    }
  }
</script>

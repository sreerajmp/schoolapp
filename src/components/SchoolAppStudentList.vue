<template>
<div v-if="loading"><h1>Loading...</h1></div>
  <div v-if="!loading"
    class="grid grid-cols-1 gap-6 mt-4 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 justify-items-center"
  >
    <SchoolAppStudentCard v-for="(student, index) in students" :key="index" :student="student" :class_rooms="class_rooms"/>
  </div>
</template>

<script >
import axios from 'axios'
import SchoolAppStudentCard from '../components/SchoolAppStudentCard.vue'
export default {
  components: {
    SchoolAppStudentCard
  },
  data () {
    return {
      students: [],
      class_rooms: [],
      res: null,
      loading: true,
      error: null
    }
  },
  methods: {
    async fetchList () {
      const response = await axios.get('https://hamon-interviewapi.herokuapp.com/students/?api_key=Aaf59')
      localStorage.setItem('student_list', JSON.stringify(response.data.students))
      this.students = JSON.parse(localStorage.getItem('student_list'))
    },
    async fetchClassList () {
      await axios.get('https://hamon-interviewapi.herokuapp.com/classrooms/?api_key=Aaf59').then(resp => {
        resp.data.classrooms.forEach(element => {
          axios.get('https://hamon-interviewapi.herokuapp.com/classrooms/' + element.id + '?api_key=Aaf59').then(res => {
            if (res.data.subject) {
              this.class_rooms.push(res.data)
              localStorage.setItem('classroomsSubject', JSON.stringify(this.class_rooms))
              this.loading = false
            }
          })
        })
      })
    }
  },
  mounted () {
    this.fetchList()
    this.fetchClassList()
  }
}
</script>

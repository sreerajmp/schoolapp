<template>
<div v-if="loading"><h1>Loading...</h1></div>
  <div v-if="!loading"
    class="grid grid-cols-1 gap-6 mt-4 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 justify-items-center"
  >
    <SchoolAppStudentCard v-for="(student, index) in students" :key="index" :student="student" />
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
      console.log('fetchList')
      const response = await axios.get('https://hamon-interviewapi.herokuapp.com/students/?api_key=Aaf59')
      localStorage.setItem('student_list', JSON.stringify(response.data.students))
      this.students = JSON.parse(localStorage.getItem('student_list'))
      console.log('res:', response.data.students)
    },
    async fetchClassList () {
      console.log('log:', this.class_rooms)
      await axios.get('https://hamon-interviewapi.herokuapp.com/classrooms/?api_key=Aaf59').then(resp => {
        resp.data.classrooms.forEach(element => {
          axios.get('https://hamon-interviewapi.herokuapp.com/classrooms/' + element.id + '?api_key=Aaf59').then(res => {
            console.log('ressss:', res.data)
            if (res.data.subject) {
              this.class_rooms.push(res.data)
              localStorage.setItem('classroomsSubject', JSON.stringify(this.class_rooms))
            }
          })
        })
        this.loading = false
        console.log('res.dat:', this.class_rooms)
      })
    }
  },
  mounted () {
    this.fetchList()
    this.fetchClassList()
  }
}
</script>

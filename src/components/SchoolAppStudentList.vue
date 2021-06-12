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
      res: null,
      loading: true,
      error: null
    }
  },
  methods: {
    async fetchList () {
      console.log('fetchList')
      const response = await axios.get('https://hamon-interviewapi.herokuapp.com/students/?api_key=Aaf59')
      this.students = response.data.students
      this.loading = false
      console.log('res:', response.data.students)
    }
  },
  mounted () {
    this.fetchList()
  }
}
</script>

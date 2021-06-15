<template>
<div v-if="loading"><h1>Loading...</h1></div>
  <div v-if="!loading"
    class="grid grid-cols-1 gap-6 mt-4 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 justify-items-center"
  >
    <SchoolAppClassCard v-for="(classroom, index) in classrooms" :key="index" :classroom="classroom" :students_list="students_list" />
  </div>
</template>

<script >
import axios from 'axios'
import SchoolAppClassCard from './SchoolAppClassCard.vue'
export default {
  components: {
    SchoolAppClassCard
  },
  data () {
    return {
      classrooms: [],
      students_list: [],
      res: null,
      loading: true,
      error: null
    }
  },
  methods: {
    async fetchList () {
      console.log('fetchList')
      const response = await axios.get('https://hamon-interviewapi.herokuapp.com/classrooms/?api_key=Aaf59')
      this.classrooms = response.data.classrooms
      console.log('resClass:', this.classrooms)
      this.loading = false
    }
    // async getSudentList () {
    //   await axios.get('https://hamon-interviewapi.herokuapp.com/students/?api_key=Aaf59').then(response => {
    //     this.students_list = response.data.students
    //     localStorage.setItem('students_list', JSON.stringify(response.data.students))
    //     this.loading = false
    //   })
    // }
  },
  mounted () {
    this.fetchList()
    // this.getSudentList()
  }
}
</script>

<template>
<div v-if="loading"><h1>Loading...</h1></div>
  <div v-if="!loading"
    class="grid grid-cols-1 gap-6 mt-4 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 justify-items-center"
  >
    <SchoolAppSubjectCard v-for="(subject, index) in subjects" :key="index" :subject="subject" />
  </div>
</template>

<script >
import axios from 'axios'
import SchoolAppSubjectCard from './SchoolAppSubjectCard.vue'
export default {
  components: {
    SchoolAppSubjectCard
  },
  data () {
    return {
      subjects: [],
      res: null,
      loading: true,
      error: null
    }
  },
  methods: {
    async fetchList () {
      const response = await axios.get('https://hamon-interviewapi.herokuapp.com/subjects/?api_key=Aaf59')
      this.loading = false
      this.subjects = response.data.subjects
    }
  },
  mounted () {
    this.fetchList()
  }
}
</script>

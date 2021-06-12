<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <SchoolAppStudentList></SchoolAppStudentList>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import SchoolAppStudentList from '@/components/SchoolAppStudentList.vue' // @ is an alias to /src

@Options({
  components: {
    SchoolAppStudentList
  }
})
export default class Home extends Vue {}
</script>

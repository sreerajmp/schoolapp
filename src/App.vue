<template>
  <SchoolAppHeader/>
  <router-view/>
<!-- <SchoolAppStudentList :students="students"/> -->
  <SchoolAppFooter/>
</template>
<script>
import axios from 'axios'
import SchoolAppHeader from './components/SchoolAppHeader.vue'
import SchoolAppFooter from './components/SchoolAppFooter.vue'
import SchoolAppStudentList from './components/SchoolAppStudentList.vue'

export default {
  components: {
    SchoolAppHeader,
    SchoolAppFooter
  }
}
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Gloria+Hallelujah');
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#button {
  color: red;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

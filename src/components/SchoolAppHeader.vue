<template>
  <header>
    <router-link to="/"><p>My School Application</p></router-link>
    <nav>
      <ul>
        <li><router-link to="/">Home</router-link></li>
        <li><router-link to = "/classList">Classrooms List</router-link></li>
        <li><router-link to = "/studentList">Student List</router-link></li>
        <li><router-link to = "/subjectList">Subject List</router-link></li>
      </ul>
    </nav>
  </header>
</template>

<style lang="scss">
header {
    font-family: 'Grand Slang', sans-serif;
    font-weight: 400;
    line-height: 1.25;
    display: flex;
    border-bottom: 1px solid #ccc;
    padding: .5rem 1rem;

    p {
      margin-left: 1rem;
    }
  }

  nav {
    margin-left: auto;

    ul {
      list-style: none;
    }

    ul li {
      display: inline-flex;
      margin-left: 1rem;
    }
  }
</style>

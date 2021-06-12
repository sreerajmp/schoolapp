<template>
  <section class="p-4 text-justify rounded-lg shadow-lg bg-gray-50 w-80">
    <div class="h-30">
      <p class="font-bold ">
        Room:{{ classroom.name }}
      </p>
      <p>
        layout:{{ classroom.layout }}
      </p>
      <button v-if="more===false" v-on:click="moreDetails" style="color:green; font-size:13px">Show more...</button>
      <div v-if="more===true">
      <p class="mt-2 text-gray-700 line-clamp-4">
        Size:{{ classroom.size }}
      </p>
      <p class="mt-2 text-gray-700 line-clamp-4" >
        subject:{{ classSub }}
      </p>
      <div v-if="classStud">
      Student:{{ classStud }}<button v-on:click="removeStudent" style="color:red;font-size:10px">&emsp;&emsp;&emsp;<span >remove</span></button>
      </div>
    <div>
      <p class="mt-2 text-gray-700 line-clamp-4">
        <label>Assign Subject:</label>
      <select v-model="sub" @change="assignSubject(sub)">
        <option v-for="(subject,index) in subjects" :key="index" v-bind:value="subject"> {{subject.name}} </option>
      </select>
      </p>
    </div>
    <div v-if="classSub">
      <p class="mt-2 text-gray-700 line-clamp-4">
        <label>Assign Student:</label>
      <select v-model="stud" @change="assignStudent(stud)">
        <option v-for="(student,index) in students_list_new" :key="index" v-bind:value="student"> {{student.name}} </option>
      </select>
      </p>
    </div>
    </div>
    <button v-if="more===true" v-on:click="moreDetails" style="color:blue; font-size:13px">Hide...</button>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      students_list_new: JSON.parse(localStorage.getItem('students_list')),
      more: false,
      classSub: null,
      classStud: null,
      sub: {},
      stud: {},
      subjects: [{ id: 1, name: 'History' }, { id: 2, name: 'Mathematics' }, { id: 3, name: 'Social Science' }, { id: 4, name: 'Physics' }, { id: 5, name: 'Chemistry' }, { id: 6, name: 'Biology' }]
    }
  },
  props: {
    classroom: {
      type: Object,
      required: true
    },
    students_list: {
      type: Array,
      required: true
    }
  },
  methods: {
    async removeStudent () {
      this.classStud = null
    },
    async moreDetails () {
      this.more = !this.more
      await axios.get('https://hamon-interviewapi.herokuapp.com/classrooms/' + this.classroom.id + '?api_key=Aaf59').then(response => {
        console.log('Classss:', response.data)
        this.subjects.forEach(element => {
          if (element.id === response.data.subject) {
            this.classSub = element.name
          }
        })
      })
    },
    async assignSubject (Seletedsub) {
      await axios.patch('https://hamon-interviewapi.herokuapp.com/classrooms/' + this.classroom.id + '?api_key=Aaf59', 'subject=' + Seletedsub.id).then(response => {
        console.log('res:', response)
        if (response.status === 200 && response.data.subject === Seletedsub.id) {
          this.classSub = Seletedsub.name
        }
      })
    },
    async assignStudent (Seletedstud) {
      console.log('this.students_list::', Seletedstud)
      this.classStud = Seletedstud.name
    }
  }
}
</script>

<template>
  <section class="p-4 text-justify rounded-lg shadow-lg bg-gray-50 w-80">
    <div class="h-30">
      <p class="font-bold ">
        Name:{{ student.name }}
      </p>
      <button v-if="more===false" v-on:click="moreDetails" style="color:green; font-size:13px">Show more</button>
      <div v-if="more===true">
      <p class="mt-2 text-gray-700 line-clamp-4">
        Age:{{ student.age }}
      </p>
      <div v-if="Studclass">
      Clasroom:{{ Studclass }}<button v-on:click="removeClass" style="color:red;font-size:10px">&emsp;&emsp;&emsp;<span >remove</span></button>
      </div>
    <div>
      <p class="mt-4 text-gray-600">Email:{{ student.email}}</p>
    </div>
    <div>
      <p class="mt-2 text-gray-700 line-clamp-4">
        <label>Assign Class:</label>
        <select v-model="classSelected" @change="assignClass(classSelected)">
          <option v-for="(classess,index) in classRoomWithSubject" :key="index" v-bind:value="classess"> {{classess.name}}</option>
      </select>
      </p>
    </div>
    </div>
    </div>
    <button v-if="more===true" v-on:click="moreDetails" style="color:blue; font-size:13px">Hide...</button>
  </section>
</template>

<script>
export default {
  data () {
    return {
      classSelected: {},
      more: false,
      Studclass: null,
      classRoomWithSubject: [],
      student_list: []
    }
  },
  props: {
    student: {
      type: Object,
      required: true
    },
    class_rooms: {
      type: Array,
      required: true
    }
  },
  methods: {
    async removeClass () {
      localStorage.removeItem(this.student.id)
      this.Studclass = null
    },
    async moreDetails () {
      this.more = !this.more
    },
    async assignClass (Seleted) {
      this.Studclass = Seleted.name
      localStorage.setItem(this.student.id, Seleted.name)
    }
  },
  mounted () {
    this.classRoomWithSubject = this.class_rooms
    this.student_list = JSON.parse(sessionStorage.getItem('student_list'))
    this.Studclass = localStorage.getItem(this.student.id)
  }
}
</script>

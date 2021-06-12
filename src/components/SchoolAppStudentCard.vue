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
    <div>
      <p class="mt-4 text-gray-600">{{ student.email}}</p>
    </div>
    </div>
    </div>
    <button v-if="more===true" v-on:click="moreDetails" style="color:blue; font-size:13px">Hide...</button>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      more: false
    }
  },
  props: {
    student: {
      type: Object,
      required: true
    }
  },
  methods: {
    async moreDetails () {
      this.more = !this.more
    }
  }
}
</script>

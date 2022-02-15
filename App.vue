<template>
  <view class="container">
    <view class="cards">
      <text v-if="students.length == 0">Loading directory...</text>
      <Card v-else v-for="student in students" :key="student.email" :student="student" />
    </view>
  </view>
</template>

<script>
import axios from 'axios'

import Card from './components/Card'

export default {
    data() {
      return {
        punches: 0,
        students: []
      }
    },
    components: {
      Card
    },
    mounted() {
      axios.get('http://10.1.232.108:8081/student').then(students => {
        this.students = students.data
      })
    },
    methods: {
    },
}
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: blue;
}
</style>
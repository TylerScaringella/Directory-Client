<template>
  <view class="container">
    <view class="cards">
      <view class="filters">
        <text-input 
          :style="{height: 50, borderColor: 'gray', borderWidth: 2}"
          v-model="filter.name"
          placeholder="enter a name..."
          :on-value-change="renderedStudents = students.filter(student => student.name.toLowerCase().includes(filter.name.toLowerCase()))"
        />
        <view class="classes">
          <button 
            :on-press="updateGrad(2022)"
            title="2022"
            color="#841584"
            accessibility-label="Click to see the class of 2025"
          />
        </view>
      </view>
      <activity-indicator v-if="students.length == 0" :style="{flex: 1, justifyContent: 'center'}" size="large" color="#0000ff" />
      <scroll-view v-else :content-container-style="{contentContainer: {
        paddingVertical: 0
      }}">
        <Card v-for="student in renderedStudents" :key="student.email" :student="student" />
      </scroll-view>
    </view>
  </view>
</template>

<script>
import axios from 'axios'

import Card from './components/Card'
import { StyleSheet } from 'react-native'

export default {
    data() {
      return {
        punches: 0,
        filter: {
          name: '',
          grad: 0
        },
        form: '',
        students: [],
        renderedStudents: []
      }
    },
    components: {
      Card,
      StyleSheet
    },
    methods: {
      updateGrad(year) {
        this.filter.grad = year
      }
    },
    mounted() {
      axios.get('http://10.1.232.108:8081/student').then(students => {
        this.students = students.data
        this.renderedStudents = this.students
      })
    }
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

.cards {
  margin-top: 50px;
}
</style>
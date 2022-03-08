<template>
  <view class="container">
    <view class="cards">
      <view class="filters">
        <text-input 
          :style="{height: 50, borderColor: 'gray', borderWidth: 2}"
          v-model="filter.name"
          placeholder="enter a name..."
          :onSubmitEditing="() => renderedStudents = students.filter(student => student.name.toLowerCase().includes(filter.name.toLowerCase()))"
        />
        <view class="classes">
          <touchable-opacity 
            :style="{
              alignItems: 'center',
              backgroundColor: '#841584',
              padding: 15,
              marginBottom: 5,
              marginTop: 5
            }"
            :on-press="() => updateGrad(2022)"
            >
            <text :style="{color: '#fff'}">2022</text>
          </touchable-opacity>
          <touchable-opacity 
            :style="{
              alignItems: 'center',
              backgroundColor: '#841584',
              padding: 15,
              marginBottom: 5,
              marginTop: 5
            }"
            :on-press="() => updateGrad(2023)"
            >
            <text :style="{color: '#fff'}">2023</text>
          </touchable-opacity>
          <touchable-opacity 
            :style="{
              alignItems: 'center',
              backgroundColor: '#841584',
              padding: 15,
              marginBottom: 5,
              marginTop: 5
            }"
            :on-press="() => updateGrad(2024)"
            >
            <text :style="{color: '#fff'}">2024</text>
          </touchable-opacity>
          <touchable-opacity 
            :style="{
              alignItems: 'center',
              backgroundColor: '#841584',
              padding: 15,
              marginBottom: 5,
              marginTop: 5
            }"
            :on-press="() => updateGrad(2025)"
            >
            <text :style="{color: '#fff'}">2025</text>
          </touchable-opacity>
        </view>
      </view>
      <activity-indicator v-if="students.length == 0" :style="{flex: 1, justifyContent: 'center'}" size="large" color="#0000ff" />
      <flat-list v-else 
          :data="renderedStudents"
          :key-extractor="(item) => item.email"
          :render-item="(item) => renderItem(item)"
      />
    </view>
  </view>
</template>

<script>
import axios from 'axios'

import Card from './components/Card'
import React, { StyleSheet, Text } from 'react-native'

// Home
// const baseURL = `http://10.46.1.175:8081`
// School
const baseURL = `http://10.1.232.108:8081`

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
        this.filter.name = ''
        this.renderedStudents = this.students.filter(student => student.graduation == this.filter.grad)
      },
      renderItem(item) {
        return (<Card student={item.item} />)
      }
    },
    mounted() {
      axios.get(`${baseURL}/student`).then(students => {
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
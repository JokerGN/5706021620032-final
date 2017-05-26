<template>
  <div id="app">
  <div class="columns">
    <div class="column is-half is-offset-3">
      <h1 class="title is-1">โปรแกรมคำนวณเกรด</h1>
      <div class="field"> 
        <p class="control">
          <input class="input" type="text" placeholder="ชื่อวิชา" v-model="subject.name">
        </p>
      </div>
      <div class="field">
        <p class="control">
          <input class="input" type="text" placeholder="หน่วยกิต" v-model="subject.unit">
        </p>
      </div>
      <div class="field">
        <p class="control">
          เกรด
          <span class="select">
            <select v-model="subject.grade">
              <option>A</option>
              <option>B+</option>
              <option>B</option>
              <option>C+</option>
              <option>C</option>
              <option>D+</option>
              <option>D</option>
              <option>F</option>
            </select>
          </span>
        </p>
      </div>
      <div>
        <button class="button is-primary" @click="addSubject">Add</button>
      </div>
     <table class="table">
      <thead>
        <th>ชื่อวิชา</th>
        <th>หน่วยกิต</th>
        <th>เกรดที่ได้</th>
      </thead>
      <tbody>
        <tr v-for="subject in subjects">
          <td>{{subject.name}}</td>
          <td>{{subject.unit}}</td>
          <td>{{subject.grade}}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td>GPA : {{calGrade}}</td>
        </tr>
      </tfoot>
     </table>
    </div>
  </div>
  </div>
</template>

<script>
import 'bulma/css/bulma.css'

export default {
  name: 'app',
  data () {
    return {
      subjects: [],
      subject: {
        name: '',
        unit: '',
        grade: ''
      },
      gradeScore: 0,
      allUnit: 0,
      gpa: 0
    }
  },
  methods: {
    addSubject () {
      let vm = this
      vm.subjects.push(vm.subject)
      vm.subject = {
        name: '',
        unit: '',
        grade: ''
      }
    }
  },
  computed: {
    calGrade () {
      let vm = this
      if (vm.subjects.length !== 0) {
        let currentData = vm.subjects[vm.subjects.length - 1]
        if (currentData.grade === 'A') {
          vm.gradeScore += 4 * currentData.unit
        }
        if (currentData.grade === 'B+') {
          vm.gradeScore += 3.5 * currentData.unit
        }
        if (currentData.grade === 'B') {
          vm.gradeScore += 3 * currentData.unit
        }
        if (currentData.grade === 'C+') {
          vm.gradeScore += 2.5 * currentData.unit
        }
        if (currentData.grade === 'C') {
          vm.gradeScore += 2 * currentData.unit
        }
        if (currentData.grade === 'D+') {
          vm.gradeScore += 1.5 * currentData.unit
        }
        if (currentData.grade === 'D') {
          vm.gradeScore += 1 * currentData.unit
        }
        if (currentData.grade === 'F') {
          vm.gradeScore += 0 * currentData.unit
        }
        vm.allUnit += parseInt(currentData.unit)
      }
      vm.gpa = vm.gradeScore / vm.allUnit
      return vm.gpa.toFixed(2)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

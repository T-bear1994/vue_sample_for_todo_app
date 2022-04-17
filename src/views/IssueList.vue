<template>
  <div>
    <h1>issueリスト</h1>
    <el-button @click="getIssues()" type="success">issue取得</el-button>
    <el-row :gutter="12">
      <!-- コード１ -->
      <el-col :span="12" v-for="issue in issues" :key="issue.id">
        <el-card class="box-card" shadow="hover" style="margin: 5px 0;">
          <el-row :gutter="12">
             <!-- コード2 -->
            <el-col :span="21">{{ issue.title }}</el-col>
            <el-col :span="3">
              <el-button  @click="removeTodo(index)" type="success" icon="el-icon-check" circle></el-button>
            </el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios';

const client = axios.create({
  baseURL: 'https://api.github.com/repos/T-bear1994/vue_sample_for_todo_app',
  headers: {
    'Accept': 'application/vnd.github.v3+json',
    'Content-Type':'application/json',
  },
})



export default {
  name: 'IssueList',
  data() {
    return {
      issues: []
    }
  },
  methods: {
    getIssues() {
      client.get('https://api.github.com/repos/T-bear1994/vue_sample_for_todo_app/issues')
        .then((res) => {
          this.issues = res.data;
      })
    }
  }
}
</script>
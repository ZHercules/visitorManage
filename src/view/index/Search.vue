<template>
  <div>
  <center>
  <el-form @submit.prevent="searchUsers" class="demo-form-inline">
    <el-form-item label="姓名">
      <el-input v-model="visitorName" placeholder="姓名"></el-input>
    </el-form-item>
    <el-form-item label="联系方式">
      <el-input v-model="phone" placeholder="联系方式"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" native-type="submit">查询</el-button>
    </el-form-item>
  </el-form>
      <el-table :data="visitors" border>
        <el-table-column prop="visitorName" label="姓名"></el-table-column>
        <el-table-column prop="visitTime" label="到访日期"></el-table-column>
        <el-table-column prop="event" label="到访事由"></el-table-column>
      </el-table>
  </center>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "Search",
  data() {
    return {
      visitorName: '',
      phone: '',
      visitors:[]
    }
  },
  methods: {
    searchUsers() {
      axios.get(`/api/users?visitorName=${this.visitorName}&phone=${this.phone}`)
        .then(response => {
          this.visitors = response.data.results;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
}
</script>

<style scoped>

</style>

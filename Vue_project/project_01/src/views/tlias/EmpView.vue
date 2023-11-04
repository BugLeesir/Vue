<template>
  <div>
    <el-container style="height: 700px; border: 1px solid #eee">
      <el-header style="font-size: 40px; background-color: rgb(238, 241, 246)">tlias 智能学习辅助系统</el-header>
      <el-container>
        <el-aside width="200px" style=" border: 1px solid #eee">
          <el-menu :default-openeds="['1', '3']">
            <el-submenu index="1">
              <template slot="title"><i class="el-icon-message"></i>系统信息管理</template>
              <el-menu-item index="1-1">
                 <router-link to="/dept">部门管理</router-link>
              </el-menu-item>
              <el-menu-item index="1-2">
                  <router-link to="/emp">员工管理</router-link>  
              </el-menu-item>
            </el-submenu>
          </el-menu>
        </el-aside>
        <el-main>
          <!-- 表单 -->
          <el-form :inline="true" :model="searchForm" class="demo-form-inline">
            <el-form-item label="姓名">
              <el-input v-model="searchForm.name" placeholder="姓名"></el-input>
            </el-form-item>
            <el-form-item label="性别">
              <el-select v-model="searchForm.gender" placeholder="性别">
                <el-option label="男" value="1"></el-option>
                <el-option label="女" value="2"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="onSubmit">查询</el-button>
            </el-form-item>
          </el-form>
          <!-- 表格 -->
          <el-table :data="tableData" border>
            <el-table-column prop="id" label="编号" width="140">
            </el-table-column>
            <el-table-column prop="first_name" label="姓名" width="120">
            </el-table-column>
            <el-table-column label="图片" width="180">
              <template slot-scope="scope">
                <img :src="scope.row.avatar" alt="" style="width: 100px; height: 70px">
              </template>
            </el-table-column>
          </el-table>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      tableData: [],
      searchForm: {
        name: "",
        gender: ""
      }
    }
  },
  methods: {
    onSubmit() {
      alert('submit!');
    },
  },
  mounted() {
    // 发送请求获取数据
    axios.get('https://reqres.in/api/users?page=2').then(res => {
      this.tableData = res.data.data;
    })
  }
}

</script>


<template>
  <div>
    <!--面包屑导航区-->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item to="/home">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>权限列表</el-breadcrumb-item>
    </el-breadcrumb>

    <!--卡片视图区域-->
    <el-card>
      <el-table :data="rightsList" border stripe>
        <el-table-column label="ID" prop="id"></el-table-column>
        <el-table-column label="权限名称" prop="authName"></el-table-column>
        <el-table-column label="权限等级" prop="level">
          <template slot-scope="scope">
            <el-tag type="primary" v-if="scope.row.level === '0'">等级1</el-tag>
            <el-tag type="warning" v-else-if="scope.row.level === '1'">等级2</el-tag>
            <el-tag type="danger" v-else-if="scope.row.level === '2'">等级3</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="父权限ID" prop="pid"></el-table-column>
        <el-table-column label="路径" prop="path"></el-table-column>
      </el-table>
    </el-card>
  </div>
</template>

<script>
export default {
  name: 'Rights',
  data () {
    return {
      rightsList: [] //用户权限列表
    }
  },
  methods: {
    //获取权限列表
    getRightsList () {
      this.$http.get('rights/list').then(response => {
        const resp = response.data
        if (resp.meta.status !== 200) {
          return this.$message.error('获取权限列表失败')
        }
        this.rightsList = resp.data
      })
    }
  },
  created () {
    this.getRightsList()
  }
}
</script>

<style scoped>

</style>

<template>
  <div class="account-manage">
    <el-card class="box-card">
      <div slot="header" class="clearfix">
        <h3>账号管理</h3>
      </div>
      <div class="text item">
        <el-table
          ref="multipleTable"
          :data="accountManageData"
          tooltip-effect="dark"
          style="width: 100%"
        >
          <el-table-column type="selection" width="55"></el-table-column>
          <el-table-column prop="account" label="账号"></el-table-column>
          <el-table-column prop="userType" label="用户类型"></el-table-column>
          <el-table-column label="创建日期">
            <template slot-scope="scope">{{ scope.row.createDate }}</template>
          </el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button size="mini" type="info" @click="handleEdit(scope.$index, scope.row)">
                <i class="el-icon-edit"></i>编辑
              </el-button>
              <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">
                <i class="el-icon-delete"></i>删除
              </el-button>
            </template>
          </el-table-column>
        </el-table>
        <!-- 分页 -->
        <div class="pagination" style="margin-top:20px;">
          <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="1"
            :page-sizes="[1, 3, 5, 10]"
            :page-size="100"
            layout="total, sizes, prev, pager, next, jumper"
            :total="11"
          ></el-pagination>
        </div>
        <div style="margin-top: 20px">
          <el-button type="primary">
            <i class="el-icon-delete-solid"></i>批量删除
          </el-button>
          <el-button type="success">
            <i class="el-icon-close"></i>取消选择
          </el-button>
        </div>
      </div>
    </el-card>
  </div>
</template>
<style lang="less">
@import "./accountmanage";
</style>
<script>
export default {
  data() {
    return {
      accountManageData: [
        {
          account: "admin",
          userType: "超级管理员",
          createDate: "2020-02-01"
        }
      ]
    };
  },
  methods: {
    //编辑
    handleEdit() {},
    //删除
    handleDelete() {},
    // 分页相关
    handleSizeChange(){},
    handleCurrentChange(){}
  }
};
</script>
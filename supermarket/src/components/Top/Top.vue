<template>
  <div class="top">
    <el-row :gutter="20">
      <el-col :span="20">
        <div class="grid-content bg-purple">
          <h3 class="title">
            <i class="el-icon-s-home"></i>超市管理系统
          </h3>
        </div>
      </el-col>
      <el-col :span="4">
        <div class="grid-content bg-purple">
          <el-row>
            <!-- 头像 -->
            <el-col :span="8">
              <div class="demo-basic--circle">
                <div class="block">
                  <el-avatar :size="50" :src="accountInfo.imageUrl"></el-avatar>
                </div>
              </div>
            </el-col>
            <el-col :span="16">
              <!-- 下拉 -->
              <el-dropdown @command="handleCommand">
                <span class="el-dropdown-link">
                  {{accountInfo.account}}
                  <i class="el-icon-arrow-down el-icon--right"></i>
                </span>
                <!-- 下拉 -->
                <el-dropdown-menu slot="dropdown">
                  <el-dropdown-item command="userCenter">个人中心</el-dropdown-item>
                  <el-dropdown-item command="logout">退出系统</el-dropdown-item>
                </el-dropdown-menu>
              </el-dropdown>
            </el-col>
          </el-row>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import localStor from "@/utils/localStor.js";
export default {
  // 数据
  data() {
    return {
      accountInfo: {
        name:'',
        imageUrl:''
      },
      // 头像地址
    };
  },
  methods: {

    // 获取当前用户
    getCurrentAccount() {
      this.$http.get("account/currentaccount").then(res => {
        let { code, messsage, result } = res.data;
        if (code === 0) {
          let data = result.account;
          this.accountInfo.account = data.account;
          this.accountInfo.imageUrl='http://127.0.0.1:3001'+data.imageUrl;
          return;
        }
        this.$message.error("遇到错误，请重新登录");
        this.$router.push("/login");
        return;
      });
    },
    //退出系统
    logout() {
      localStor.remove("zsy_hy");
      this.$message({
        type: "info",
        message: "退出成功"
      });
      setTimeout(() => {
        this.$router.push("/login");
      }, 1000);
    },
    // 个人中心、退出系统
    handleCommand(command) {
      if (command === "userCenter") {
        this.$router.push("/home/personal");
        return;
      }
      this.logout();
      return;
    }
  },
  // 生命周期函数
  created() {
    this.getCurrentAccount();
  }
};
</script>

<style lang="less">
@import "./top.less";
</style>
<template>
  <div class="navbar">
    <el-menu
      default-active="1"
      class="el-menu-nav"
      mode="horizontal"
      @select="handleSelect"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b"
    >
      <el-menu-item index="1">个人主页</el-menu-item>
      <el-submenu index="2">
        <template slot="title">模拟试卷</template>
        <el-menu-item index="2-1">四六级</el-menu-item>
        <el-menu-item index="2-2">计算机二级</el-menu-item>
        <el-menu-item index="2-3">算法试题</el-menu-item>
        <el-submenu index="2-4">
          <template slot="title">编程语言</template>
          <el-menu-item index="2-4-1">C语言</el-menu-item>
          <el-menu-item index="2-4-2">Java</el-menu-item>
          <el-menu-item index="2-4-3">C#</el-menu-item>
        </el-submenu>
      </el-submenu>
      <el-menu-item index="3" disabled>我的历史</el-menu-item>
      <el-menu-item index="4">我的分享</el-menu-item>
      <div class="user-info">
        <el-dropdown>
          <div class="u-a-content">
            <img class="u-a-avatar" :src="getUser.avatar" alt="头像">
            <div class="u-a-name">
              {{getUser.name}}&nbsp;
              <i class="el-icon-caret-bottom"></i>
            </div>
          </div>

          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item @click.native="toHomePage">个人主页</el-dropdown-item>
            <el-dropdown-item @click.native="initSystem">初始化调试</el-dropdown-item>
            <el-dropdown-item @click.native="logout">登出</el-dropdown-item>

          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </el-menu>
  </div>
</template>

<script>
import { mapGetters, mapActions, mapMutations } from "vuex";

export default {
  data() {
    return {};
  },
  computed: {
    ...mapGetters(["getUser"])
  },
  methods: {
    initSystem(){
      localStorage.removeItem("ES_papers");
      this.init("clear");
      this.$notify.success({
        title: "成功",
        message: "试卷初始化成功！",
        duration: 1000
      });
      this.$router.push({ name: "home" });
    },
    logout() {
      this.init("clear");
      this.$notify.success({
        title: "成功",
        message: "登出成功！",
        duration: 1000
      });
      this.$router.push({ name: "home" });
    },
    toHomePage() {
        this.$router.push({ name: "user" });
    },
    ...mapMutations(["init"])
  }
};
</script>

<style scoped>
.navbar {
  width: 100%;

  background-color: #545c64;
  display: flex;
  justify-content: center;
}

.el-menu-nav {
  width: 1100px;
  display: flex;
  align-items: center;
}

.user-avatar {
  color: white;
}

.u-a-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
}

.u-a-content {
  display: flex;
  align-items: center;
}

.u-a-name {
  color: white;
  padding: 0 10px;
}

.user-info {
  flex: 1;
  position: relative;
}

.el-dropdown {
  display: flex;
  justify-content: flex-end;
}
</style>
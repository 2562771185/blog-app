<template>
  <el-header class="me-area" style="opacity: 0.9;background-color: #bdb494;
  ;background-size: cover;

">
    <el-row class="me-header">

      <el-col :span="2" class="me-header-left">
        <router-link to="/" class="me-title">
          <img src="../assets/img/logo.png"/>
        </router-link>
      </el-col>

      <el-col v-if="!simple" :span="12" :offset="3">
        <el-menu :router=true menu-trigger="click" active-text-color="#467b47" :default-active="activeIndex"
                 mode="horizontal" background-color="#bdb494" text-color="black" >
          <el-menu-item index="/" style="font-size: larger"> 首页</el-menu-item>
          <el-menu-item index="/category/all" style="font-size: larger">文章分类</el-menu-item>
          <el-menu-item index="/tag/all" style="font-size: larger">标签</el-menu-item>
          <el-menu-item index="/archives" style="font-size: larger">文章归档</el-menu-item>

          <el-col :span="4"  >
            <el-menu-item index="/write" style="font-size: larger;"><i class="el-icon-edit" ></i>写文章</el-menu-item>
          </el-col>
          <el-col :span="8">
            <el-menu mode="horizontal" active-text-color="#5FB878" background-color="#bdb494" text-color="black">
              <el-menu-item>
                <template>
                  <el-autocomplete
                    v-model="search"
                    :fetch-suggestions="querySearchAsync"
                    placeholder="请输入查找内容"
                    @select="handleSelect"
                  >
                  </el-autocomplete>
                </template>
              </el-menu-item>
            </el-menu>
          </el-col>
        </el-menu>

      </el-col>


      <template v-else>
        <slot></slot>
      </template>

      <el-col :span="4" >
        <el-menu :router=true menu-trigger="click" mode="horizontal" background-color="#bdb494">
          <template v-if="!user.login">
            <el-menu-item index="/login">
              <el-button type="info">登录</el-button>
            </el-menu-item>
            <el-menu-item index="/register">
              <el-button type="info">注册</el-button>
            </el-menu-item>
          </template>

          <template v-else>
            <el-submenu index>
              <template slot="title">
                <img class="me-header-picture" :src="user.avatar"/>
              </template>
              <el-menu-item index @click="logout" style="color: #467b47"><i class="el-icon-back"></i>退出</el-menu-item>
            </el-submenu>
          </template>
        </el-menu>
      </el-col>

    </el-row>
  </el-header>
</template>

<script>
import {searchArticle} from "../api/article";

export default {
  name: 'BaseHeader',
  props: {
    activeIndex: String,
    simple: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {search: '',}
  },
  computed: {
    user() {
      let login = this.$store.state.account.length != 0
      let avatar = this.$store.state.avatar
      return {
        login, avatar
      }
    }
  },
  methods: {
    logout() {
      let that = this
      this.$store.dispatch('logout').then(() => {
        this.$router.push({path: '/'})
        that.$message({message: "退出成功", type: 'success', showClose: true});
      }).catch((error) => {
        if (error !== 'error') {
          that.$message({message: error, type: 'error', showClose: true});
        }
      })
    },
    querySearchAsync(queryString,cb){
      searchArticle(this.search).then((res)=>{
        const results = [];
        if (res.success){
          for(const item of res.data){
            results.push({id:item.id,value:item.title})
          }
        }

        //cb是回调函数，返回筛选出的结果数据到输入框下面的输入列表
        cb(results);
      })
    },
    handleSelect(item){
      this.$router.push({path:'/view/'+item.id})
    }
  }
}
</script>

<style>

.el-header {
  position: fixed;
  z-index: 1024;
  min-width: 100%;
  box-shadow: 0 2px 3px hsla(0, 0%, 7%, .1), 0 0 0 1px hsla(0, 0%, 7%, .1);
}

.me-title {
  margin-top: 10px;
  font-size: 24px;
}

.me-header-left {
  margin-top: 10px;
}

.me-title img {
  max-height: 2.4rem;
  max-width: 100%;
}

.me-header-picture {
  width: 36px;
  height: 36px;
  border: 1px solid #ddd;
  border-radius: 50%;
  vertical-align: middle;
  background-color: #5fb878;
}
</style>

<template>
  <el-container>
    <el-header>
      <el-row>
        <el-col :span="6">
          <Bird style="float:left;padding-top:10px"/>
        </el-col>
        <el-col :span="6">
          <el-input size="small" placeholder="请输入搜索内容" v-model="keyword">
            <i class="el-icon-edit el-input__icon" slot="suffix"></i>
          </el-input>
        </el-col>
        <el-col :span="6">
          <el-menu style="height:59px" mode="horizontal">
            <el-menu-item index="1"><span><i class="el-icon-house"></i>首页</span></el-menu-item>
            <el-menu-item index="2">归档</el-menu-item>
            <el-menu-item index="3">分类</el-menu-item>
            <el-menu-item index="4">关于</el-menu-item>
          </el-menu>
        </el-col>
        <el-col style="text-align: right; font-size: 12px" :span="6">
          <el-dropdown>
            <span class="avatar"></span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>用户登录</el-dropdown-item>
              <el-dropdown-item>用户注册</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <!-- <el-aside width="250px" style="background-color: rgb(238, 241, 246)">
        <h2>About Me</h2>
        <h5>Photo of me:</h5>
        <div class="fakeimg me_img" style="height:200px;">Image</div>
        <p>明天又是充满绝望的一天</p>
      </el-aside>-->
      <el-container>
        <el-main>
          <el-card v-for="item in list" :key="item.article_id" class="card-item" shadow="hover">
            <el-divider content-position="center">
              <span class="card-item-title">{{item.article_title}}</span>
              <span>{{formatDate(new Date(item.article_date), 'yyyy-MM-dd hh:mm:ss')}}</span>
            </el-divider>
            <!-- Markdown Viewer -->
            <TuiEditorViewer :value="item.article_content"/>
          </el-card>
          <div id="top">
            <!-- Text Editor -->
            <!-- <TuiEditor mode="markdown" preview-style="vertical" height="300px"/> -->
          </div>
        </el-main>
      </el-container>
    </el-container>
  </el-container>
</template>

<script>
import Logo from "~/components/Logo.vue";
import Bird from "~/components/Bird";
import { formatDate } from "../utils/index.js";
import axios from "axios";
export default {
  data() {
    return {
      content: `'Hello World!'`,
      tableData: [],
      formatDate,
      keyword: "",
      list: []
    };
  },
  components: {
    Logo,
    Bird
  },
  mounted() {
    this.getPostList();
  },
  methods: {
    getPostList() {
      axios.get(`http://149.28.161.252:3000/post/list`).then(res => {
        console.log("xx", res.data.data);
        this.list = res.data.data;
      });
    }
  }
};
</script>


<style>
.el-header {
  background-color: #fff;
  color: #333;
  border: 1px solid #ebeef5;
  line-height: 58px;
}

.el-aside {
  color: #333;
}
.avatar {
  vertical-align: middle;
  width: 45px;
  height: 45px;
  border-radius: 50%;
  display: inline-block;
  background: pink;
}
.fakeimg {
  background-color: #aaa;
  width: 100%;
  padding: 20px;
}
.me_img {
  background-image: url(../assets/me.jpg);
  background-size: cover;
  width: 100%;
}
.card-item {
  /* background: rgb(240, 249, 235); */
  margin-bottom: 20px;
}
.card-item-title {
  font-size: 18px;
  font-weight: 700;
  margin-right: 10px;
}
</style>


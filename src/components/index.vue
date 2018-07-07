<template>
<div>
    <el-menu
    :default-active="activeIndex2"
    class="el-menu-demo"
    mode="horizontal"
    background-color="#545c64"
    text-color="#fff"
    active-text-color="#ffd04b">
    <el-menu-item index="1">
        考试中心
    </el-menu-item>
    </el-menu>
  <el-tabs v-model="activeName2" tab-position='left' type="card">
    <el-tab-pane label="随机出题" name="first">
        <el-button class="ref-btn" @click="_getSubjectList" type="success" round><i class="el-icon-refresh"></i></el-button>
        <el-table
            :data="Subjects"
            style="width: 100%">
            <el-table-column
                prop="content">
            </el-table-column>
            </el-table>
        </el-tab-pane>
    <el-tab-pane label="添加题库" name="second">
        <el-container class="add-answer">
            <el-header>输入题目内容</el-header>
                <el-input
                type="textarea"
                :rows="5"
                placeholder="请输入内容"
                v-model="textarea">
                </el-input>
            <el-footer>
                <el-button type="success" round @click="_setSubjectList">Submit</el-button>
            </el-footer>
        </el-container>
    </el-tab-pane>
  </el-tabs>
</div>
</template>

<script>
import axios from "axios";
import Qs from 'qs'
export default {
  name: "index",
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
      activeName2: "first",
      textarea: "",
      Subjects: []
    };
  },
  created() {
    this._getSubjectList();
  },
  methods: {
    open() {
         this.$message({
          message: '问题添加成功',
          type: 'success'
        });
    },
    _getSubjectList() {
      const url = "/getAnswerList"; 
      axios.get(url).then(res => {
        this.Subjects=res.data;
        });
    },
     _setSubjectList() {
       let param = new URLSearchParams()
       param.append('content', this.textarea)
       let data={
         'content': this.textarea
       }
       if(!this.textarea) return
      //   axios({
      //     url:'/setAnswer',
      //     method: 'post',
      //     headers:{
      //       'Content-Type':'application/x-www-form-urlencoded'
      //     },
      //     data:{
      //       'content': this.textarea
      //     },
      //     transformRequest: [function (data) {
      //       let ret = ''
      //       for (let it in data) {
      //         ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&'
      //       }
      //       console.log(ret.slice(0,ret.length-1))
      //       return ret.slice(0,ret.length-1)
      //     }]

      //   }).then((res)=>{
      //     console.log(res)
      //  })
      //const url = `/setAnswer?content=${this.textarea}`; 
      const url="/setAnswer"
      //这里用post请求 后台接收不到请求的参数
      axios.post(url,data).then(res => {
       //console.log(res.data)
          if(res.data.status===0){
            this.open();
            this.textarea='';
          }
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.add-answer {
  padding: 30px;
}
.ref-btn {
  float: left;
  margin-top: 20px;
  margin-left: 20px;
}
.el-header,
.el-footer {
  background-color: rgb(84, 92, 100);
  color: rgb(255, 208, 75);
  text-align: center;
  line-height: 60px;
}

.el-aside {
  background-color: #d3dce6;
  color: #333;
  text-align: center;
  line-height: 200px;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
  text-align: center;
  line-height: 160px;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}
</style>

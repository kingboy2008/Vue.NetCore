<template>
  <div class="view-model-content" style="width: 100%;
    display: inline-block;
    height: 99%;">
    <el-scrollbar style="height:100%;">
      <div class="links">
        <div
          class="item"
          :color="activedIndex==index?'red':'#2d8cf0'"
          :class="{actived:index==activedIndex}"
          v-for="(item,index) in timeline"
          :key="index"
        >
          <span @click="change(item,index)">{{item.text}}</span>
        </div>
      </div>
      <div>
        <div class="content">
          <!-- <Divider>{{text}}</Divider> -->
          <router-view></router-view>
        </div>
      </div>
    </el-scrollbar>
  </div>
</template>
<script>
export default {
  methods: {
    change(item, index) {
      if (item.text == "框架介绍") {
        window.open("https://www.cnblogs.com/-clouds/p/11633786.html");
        return;
      }
      if (item.path == "#") {
        return this.$Message.error("框架1.0文档正在整理中...");
      }
      this.activedIndex = index;
      this.text = item.text;
      this.$router.push({ path: item.path });
    }
  },
  created() {
    let path = this.$route.path;
    for (let index = 0; index < this.timeline.length; index++) {
      if (this.timeline[index].path == path) {
        this.activedIndex = index;
      }
    }
    this.text = this.timeline[this.activedIndex].text;
    this.$Message.error("开发文档已在整理中。。。");
  },
  data() {
    return {
      text: "",
      activedIndex: 0,
      timeline: [
          {
          text: "QQ群：还没想好!",
          path: "#",
          actived: false
        },
        {
          text: "返回首页",
          path: "/home",
          actived: false
        },
        {
          text: "项目启动",
          path: "/document/guide",
          actived: false
        },
        {
          text: "代码生成",
          path: "/document/coder",
          actived: false
        },
        {
          text: "组件api",
          path: "/document/api",
          actived: false
        },
        {
          text: "前端开发",
          path: "/document/vueDev",
          actived: false
        },
        {
          text: "后台开发",
          path: "/document/netCoreDev",
          actived: false
        },
        {
          text: "H5开发",
          path: "/app/guide",
          actived: false
        },
        {
          text: "常见问题",
          path: "/document/issue",
          actived: false
        },
        {
          text: "更新记录",
          path: "/document/log",
          actived: false
        }
      ]
    };
  },
  watch: {
    "$route.path": function(newVal, oldVal) {
      //  var navItem = this.getNavigation(this.selectId);
      // this.activedIndex=2;
      //  console.log(navItem.name);
    }
  }
};
</script>
<style lang="less" scoped>

.links {
  display: flex;
  font-size: 15px;
  position: fixed;
  z-index: 9999;
  width: 100%;
  background: black;
  box-shadow: 0px 0px 10px #524747;
  > .item {
    position: relative;
    text-align: center;
    line-height: 55px;
    // padding: 10px;
    /* float: right; */
    flex: 1;
    color: #b1b0b0;
  }
  > .item:hover {
    cursor: pointer;
    color: white;
  }
  .actived {
    color: white;
    font-weight: bold;
    span {
      border-bottom: 2px solid #fff;
    }
  }
  span {
    height: 100%;
    position: relative;
    padding: 17px;
  }
}

.affix {
  left: 50px;
  position: fixed;
  top: 50px;
  padding: 20px;
  border-right: 1px solid #d6d3d3;
  .actived {
    color: #ed4014;
    font-weight: bold;
  }
  li:hover {
    cursor: pointer;
  }
}
.content {
  position: relative;

  height: 100%;
  max-width: 1200px;
  left: 0;
  right: 0;
  margin: 0 auto;
  padding: 10px;
  padding-top: 80px;
}
</style>
<style scoped>
.view-model-content >>> .el-scrollbar > .el-scrollbar__wrap {
  overflow-x: hidden;
}
</style>
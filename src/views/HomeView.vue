<template>
    <el-container style="min-height: 100vh;">
      <div>
        <el-aside :width="sideWidth + 'px'" style="background-color: rgb(238, 241, 246); height: 100%;box-shadow: 2px 0 6px rgb(0 21 41 / 35%)">
          <el-menu :default-openeds="['1', '3']" style="min-height: 100% ;overflow-x:hidden "
                   background-color="rgb(176,224,230)"
                   text-color="fff"
                   active-text-color="#ffd04b"
                   :collapse-transition="false"
                   :collapse="isCollapse"
          >
            <div style="height: 60px; line-height: 60px;text-align: center">
            <img src="../assets/logo.png" alt="" style="width: 15px;position: relative;top: 3px ;margin-right: 5px" >
              <b style="color: black" v-show="logoTextShow">水产公司管理系统</b>
            </div>
            <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-user-solid"></i>
                <span>导航一</span>
              </template>
              <el-menu-item-group>
                <template slot="title">分组一</template>
                <el-menu-item index="1-1">选项1</el-menu-item>
                <el-menu-item index="1-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="1-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="1-4">
                <template slot="title">选项4</template>
                <el-menu-item index="1-4-1">选项4-1</el-menu-item>
              </el-submenu>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title">
                <i class="el-icon-menu"></i>
                <span>导航二</span>
              </template>
              <el-menu-item-group>
                <template slot="title">分组一</template>
                <el-menu-item index="2-1">选项1</el-menu-item>
                <el-menu-item index="2-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="2-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="2-4">
                <template slot="title">选项4</template>
                <el-menu-item index="2-4-1">选项4-1</el-menu-item>
              </el-submenu>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>导航三</span>
              </template>
              <el-menu-item-group>
                <template slot="title">分组一</template>
                <el-menu-item index="3-1">选项1</el-menu-item>
                <el-menu-item index="3-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="3-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="3-4">
                <template slot="title">选项4</template>
                <el-menu-item index="3-4-1">选项4-1</el-menu-item>
              </el-submenu>
            </el-submenu>
          </el-menu>
        </el-aside>
      </div>
      <el-container>
        <el-header style=" font-size: 12px; border-bottom:1px solid #ccc; line-height:60px;display:flex">
          <div style="flex: 1 ; font-size: 18px " >
            <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
          </div>
          <el-dropdown style="width: 70px">
            <span>王小虎</span><i class="el-icon-arrow-down" style="margin-left:5px "></i>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人信息</el-dropdown-item>
              <el-dropdown-item>退出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-header>

        <el-main>
          <div style="margin: 10px 0">
          <el-input style="width: 200px" placeholder="请输入名称" suffix-icon="el-icon-search" ></el-input>
            <el-input style="width: 200px" placeholder="请输入邮箱" suffix-icon="el-icon-message" class="ml-5"></el-input>
            <el-input style="width: 200px" placeholder="请输入地址" suffix-icon="el-icon-position" class="ml-5"></el-input>
          <el-button class="ml-5" type="primary">搜索</el-button>
          </div>
          <div style="margin: 10px 0">
          <el-button type="primary">新增<i class="el-icon-circle-plus-outline"></i></el-button>
            <el-button type="danger">批量删除<i class="el-icon-circle-remove-outline"></i></el-button>
            <el-button type="danger">导入<i class="el-icon-circle-remove-outline"></i></el-button>
            <el-button type="danger">批量删除<i class="el-icon-circle-remove-outline"></i></el-button>
          </div>
          <el-table :data="tableData" border stripe header-cell-class-name="headerBg">
            <el-table-column prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
          </el-table>
          <div style="padding: 10px 0">
            <el-pagination
                :page-sizes="[5, 10, 15, 20]"
                :page-size="10"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
            </el-pagination>
          </div>
        </el-main>
      </el-container>
    </el-container>
</template>

<script>

export default {
  name: 'HomeView',
  data() {
    const item = {
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    };
    return {
      tableData: Array(10).fill(item),
      collapseBtnClass: 'el-icon-s-fold',
      isCollapse: false,
      sideWidth: 200,
      logoTextShow: true  //默认显示
    }
  },methods: {
    collapse   (){  //点击收缩按钮触发
     this.isCollapse = !this.isCollapse
      if (this.isCollapse){
        this.sideWidth = 64
        this.collapseBtnClass='el-icon-s-unfold'
        this.logoTextShow = false
      }else{  //点击展开效果
        this.sideWidth = 200
        this.collapseBtnClass = 'el-icon-s-fold'
        this.logoTextShow = true
      }
    }
  }
}
</script>

<style>
/*.el-menu-version-demo:not(.el-menu--collapse){
  wdith: 200px;
  height: 100%;
}
.el-menu-version-demo{
  transition :width 1s;
}*/
.headerBg{
  background-color:#cccccc !important;
}
</style>

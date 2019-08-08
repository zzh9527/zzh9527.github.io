---
layout: post
title: " 基于vue+element员工管理系统之角色管理"
subtitle: "Role management of employee management system based on Vue + element"
author: "zzh"
header-img: "img/post-bg-halting.jpg"
catalog: true
tags:
  - vue
  - 技术
---

> [Element-UI](https://element.eleme.cn/#/zh-CN)

负责员工管理功能
![](/img/vue.png)

## 功能点

该功能点包括：点击角色:显示角色功能、搜索角色功能、添加角色功能、

点击对应的角色时：右边显示对应的角色下的人员信息。根据用户名和部门搜索、分页

点击批量分配：显示非本角色下的所有人员信息，勾选所需人员，可添加到本角色下。

## 搭建过程

先是利用element-ul搭建静态页面，主要用到el-row、el-col、aside el-input el-button，对应的弹框使用动态组件，
弹窗主要写在组件中

## 问题总结

1、角色编辑:在父组件传数据到子组件中，更改子组件信息，会报错。
原因分析: vue父组件向子组件通过props传值时，在子组件props接受到的属性值不能被改变

解决方法：我们可以通过watch来监听props的属性值，然后赋值给data里面的属性，标签属性就可以绑定data里面的属性值
> [参考CSDN](https://blog.csdn.net/dreamer_jack/article/details/88355588)

```py
<el-input  placeholder="请输入" style="width: 45%;" v-model="roleName"></el-input>
<el-input v-model="comments" placeholder="请输入"></el-input>
props: {
    cur_roleName: String,
    cur_dec: String,
    selectIds_sys: Array,
    permission: Array,
    cur_itemId: Number
  },
  watch: {
    cur_roleName (value) {
      this.roleName = value
    },
    cur_dec (value) {
      this.comments = value
    }
  },
data () {
    return {
      roleName: this.cur_roleName,
      comments: this.cur_dec,
	}
}
```
2、权限信息的显示
checkrole.vue如下：
```py
<el-tree
  ref="trees"
  :data="permission"
  node-key="id"
  :props="props"
  :default-checked-keys="selectIds_sys"
  show-checkbox
  @node-click="handleNodeClick">
</el-tree>
props: {
    dialogEditShow: Boolean,
    cur_roleName: String,
    cur_dec: String,
    selectIds_sys: Array,
    permission: Array
},
```
main.vue如下：
```py
findAllPurview (item) { // item:点击后，对应该item的所有信息/roles里的某个角色的信息
      this.cur_sysPurviewMenus = item.sysPurviewMenus
      var selectId = []
      this.cur_sysPurviewMenus.forEach(row => {
        selectId.push(row.id)
      })
      this.selectIds_sys = selectId
      // 显示所有的权限
      this.$http.post('/blueWhale-service/purview/findAllPurview', {}, {}).then(({ data }) => {
        this.permission = data
      })
      this.cur_dialogVisible = true
    },
```





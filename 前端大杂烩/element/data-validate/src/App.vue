<template>
  <el-container style="height: 700px; border: 1px solid #eee">
    <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
      <el-menu :default-openeds="['1']" @select="handleSelect">
        <el-submenu index="1">
          <template slot="title"
            ><i class="el-icon-message"></i>导航一
          </template>
          <el-menu-item index="1-1">选项1</el-menu-item>
          <el-menu-item index="1-2">选项2</el-menu-item>
        </el-submenu>
        <el-menu-item index="2">
          <template slot="title"><i class="el-icon-menu"></i>导航二</template>
        </el-menu-item>
        <el-menu-item index="3">
          <template slot="title"
            ><i class="el-icon-setting"></i>导航三
          </template>
        </el-menu-item>
        <el-button type="primary" @click="handleClick">父组件方法</el-button>
      </el-menu>
    </el-aside>

    <el-container>
      <el-main>
        <component :is="currentComponents" ref="child"></component>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import GroupOne from "@/components/GroupOne.vue";
import GroupTwo from "@/components/GroupTwo.vue";
import ItemOne from "@/components/ItemOne.vue";
import ItemTwo from "@/components/ItemTwo.vue";
import ItemThree from "@/components/ItemThree.vue";

export default {
  name: "App",
  components: {
    GroupOne,
    GroupTwo,
    ItemOne,
    ItemTwo,
    ItemThree,
  },
  computed: {
    currentComponents() {
      return this.componentMap[this.currentIndex];
    },
  },
  data() {
    return {
      currentIndex: "1",
      componentMap: {
        1: "ItemOne",
        "1-1": "GroupOne",
        "1-2": "GroupTwo",
        2: "ItemTwo",
        3: "ItemThree",
      },
    };
  },
  methods: {
    handleSelect(index) {
      if (this.$refs.child.handleValidForm())
        this.currentIndex = index;
    },
    handleClick() {
      this.$refs.child.changeMsg("Parent");
    },
  },
};
</script>

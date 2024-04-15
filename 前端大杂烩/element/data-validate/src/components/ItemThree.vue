<template>
  <div>
    <h1>导航三</h1>
    <p>
      响应内容: <span style="color: #e86666">{{ msg }}</span>
    </p>
    <el-button type="primary" @click="changeMsg('Child')">子组件方法</el-button>
  </div>
</template>

<script>
export default {
  name: "ItemThree",
  data() {
    return {
      msg: "当前没有响应内容！",
    };
  },
  methods: {
    changeMsg(owner) {
      this.msg = `${owner} 组件改变了响应内容！`
    },
    handleValidForm() {
      return true
    },
  }
};
</script>

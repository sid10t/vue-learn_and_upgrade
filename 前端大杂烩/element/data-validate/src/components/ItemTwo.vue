<template>
  <el-form
    ref="form"
    :model="form"
    :rules="rules"
    label-width="100px"
    label-position="left"
  >
    <h1>导航二</h1>

    <el-form-item label="姓名" prop="name">
      <el-input v-model="form.name" style="width: 200px"></el-input>
    </el-form-item>
    <el-form-item label="性别" prop="sex">
      <el-radio-group v-model="form.sex">
        <el-radio label="0">男</el-radio>
        <el-radio label="1">女</el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item label="食物" prop="food">
      <el-select v-model="form.food" placeholder="请选择喜欢吃的食物">
        <el-option
          v-for="item in options"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        >
        </el-option>
      </el-select>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="handleValidForm">提交</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  name: "ItemTwo",
  data() {
    return {
      form: {
        name: null,
        sex: null,
        food: null,
      },
      rules: {
        name: [{ required: true, message: "请输入姓名", trigger: "blur" }],
        sex: [{ required: true, message: "请选择性别", trigger: "change" }],
        food: [
          { required: true, message: "请选择喜欢吃的食物", trigger: "change" },
        ],
      },
      options: [
        {
          value: "选项1",
          label: "黄金糕",
        },
        {
          value: "选项2",
          label: "双皮奶",
        },
        {
          value: "选项3",
          label: "蚵仔煎",
        },
        {
          value: "选项4",
          label: "龙须面",
        },
        {
          value: "选项5",
          label: "北京烤鸭",
        },
      ],
    };
  },
  methods: {
    submitForm() {
      this.$confirm("是否提交表单?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      })
        .then(() => {
          this.$message({
            type: "success",
            message: "提交成功!",
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消提交",
          });
        });
    },
    handleValidForm() {
      let flag = false
      this.$refs.form.validate((valid) => {
        if (valid) {
          flag = true
          this.submitForm()
        }
      });
      return flag
    },
  },
};
</script>

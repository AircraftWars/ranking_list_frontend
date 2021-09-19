<template>
  <div>
<!--    <el-container>-->
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
      <el-form-item label="用户名" prop="username">
        <el-input v-model="ruleForm.username"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input v-model="ruleForm.password"></el-input>
      </el-form-item>


      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">登陆</el-button>
        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>
    </el-form>
<!--    </el-container>-->
  </div>
</template>

<script>
import request from "../utils/request";

  export default {
    created() {

    },
    data() {
    return {
      ruleForm: {
        id: '1',
        name: '',
        password: '',
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
        ],
      }
    };
  },
  methods: {
    submitForm(formName) {
      const _this = this
      this.$refs[formName].validate((valid) => {
        if (valid) {
          // this.$axios.post('http://localhost:9090/login', this.ruleForm).then((res =>{
          //   _this.$router.push("/message")
          // }))

          request.post("http://localhost:9090/user/login", this.ruleForm).then(res =>{
            let mes = res['message']
            console.log(res)
            if(mes === '登陆成功'){
              _this.$router.push("/message")
            }
          })

        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  },
  name: "Login.vue"
}
</script>

<style scoped>

  .demo-ruleForm{
    max-width: 500px;
    margin-top: 300px;
    margin-left: 550px;
  }

</style>
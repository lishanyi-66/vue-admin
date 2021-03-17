<template>
  <div class="login">
    <div class="loginbox">
      <div class="loginleft">
        <ul class="menu-tab">
          <li
            :class="{ current: item.current }"
            v-for="item in menuTab"
            :key="item.id"
            @click="toggleMune(item)"
          >
            {{ item.text }}
          </li>
        </ul>
        <!-- 表单 -->
        <el-form
          :model="ruleForm"
          status-icon
          :rules="rules"
          ref="ruleForm"
          label-width="100px"
          class="demo-ruleForm"
          :label-position="labelPosition"
        >
          <el-form-item label="邮箱/手机号" prop="pass">
            <el-input
              type="password"
              v-model="ruleForm.pass"
              autocomplete="off"
            ></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="checkPass">
            <el-input
              type="password"
              v-model="ruleForm.checkPass"
              autocomplete="off"
            ></el-input>
          </el-form-item>
          <!-- 验证码 -->
          <el-row :gutter="16">
            <el-col :span="16"
              ><el-form-item label="验证码">
            <el-input v-model.number="ruleForm.age"></el-input>
          </el-form-item>
          </el-col>
            <el-col :span="8">
              <el-button @click="resetForm('ruleForm')">获取验证码</el-button>
              </el-col>
            
          </el-row>
          
          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')" class="btn" 
              >登录</el-button
            >
          </el-form-item>
        </el-form>
      </div>
      <div class="loginright"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "login",
  data() {
    var checkAge = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("年龄不能为空"));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error("请输入数字值"));
        } else {
          if (value < 18) {
            callback(new Error("必须年满18岁"));
          } else {
            callback();
          }
        }
      }, 1000);
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm.pass) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    return {
      labelPosition: "left",
      menuTab: [
        { text: "登录", current: true },
        { text: "注册", current: false },
      ],
      ruleForm: {
        pass: "",
        checkPass: "",
        age: "",
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        checkPass: [{ validator: validatePass2, trigger: "blur" }],
        age: [{ validator: checkAge, trigger: "blur" }],
      },
      // isActive:false
    };
  },
  methods: {
    toggleMune(data) {
      this.menuTab.forEach((e) => (e.current = false));
      data.current = true;
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
};
</script>

<style lang="less" scoped>
.login {
  height: 100vh;
  background-color: #1282e0;
  display: flex;
  justify-content: center;
  align-items: center;
  .loginbox {
    width: 50vw;
    height: 400px;
    background-color: #fff;
    display: flex;
    .loginleft {
      padding: 15px;
      flex: 5;
      .menu-tab {
        list-style: none;
        display: flex;
        font-size: 20px;
        // padding: 10px;
        border-bottom: 1px solid #eee;
        margin-bottom: 30px;
        li {
          // display: block;
          // width: 50px;
          padding: 15px 20px;

          // padding: 5px;
          // &:nth-child(2){
          //   margin-left: 30px;
          // }
        }
      }
    }
    .loginright {
      flex: 3;
      height: 100%;
      background-color: #4aa9f5;
    }
  }
  .current {
    border-bottom: 1px solid red;
    color: red;
  }
  .btn{
    width: 100%;
    display: block;
  }
}
</style>
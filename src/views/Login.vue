<template>
  <el-form
    ref="ruleFormRef"
    style="max-width: 600px"
    :model="ruleForm"
    status-icon
    :rules="rules"
    label-width="auto"
    class="demo-ruleForm"
    size="large"
  >
    <el-form-item label="Password" prop="pass">
      <el-input v-model="ruleForm.pass" type="password" show-password autocomplete="off" />
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm(ruleFormRef)"> Submit </el-button>
      <el-button @click="resetForm(ruleFormRef)">Reset</el-button>
    </el-form-item>
  </el-form>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'

const ruleFormRef = ref<FormInstance>()

const ruleForm = reactive({
  pass: ''
})

const rules = reactive<FormRules<typeof ruleForm>>({
  pass: [
    /**
     * 使用 validator 和 pattern 两种方式都可以
     */
    // { validator: validatePass, trigger: 'blur' }
    { required: true, message: 'please input your pwd!', trigger: 'blur' },
    {
      pattern:
        /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*#?&.～、,:;+–=_^：；。，？！￥~·_—`\\|/-])[A-Za-z\d$@$!%*?&#.～、,:;+–=_^：；。，？！￥~·_—`\\|/-]{8,30}/,
      message: '请输入正确的密码,长度在8-30之间，必须包含大小写字母数据和特殊符号!',
      trigger: 'blur'
    }
  ]
})

const validatePass = (rule: any, value: any, callback: any) => {
  if (value === '') {
    callback(new Error('Please input the password'))
  } else {
    const reg =
      /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*#?&.～、,:;+–=_^：；。，？！￥~·_—`\\|/-])[A-Za-z\d$@$!%*?&#.～、,:;+–=_^：；。，？！￥~·_—`\\|/-]{8,30}/
    const res = reg.test(value)
    if (res) {
      callback()
    } else {
      callback(new Error('请输入正确的密码,长度在8-30之间，必须包含大小写字母数据和特殊符号!'))
    }
  }
}

const submitForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.validate((valid) => {
    if (valid) {
      console.log('submit!')
    } else {
      console.log('error submit!')
    }
  })
}

const resetForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.resetFields()
}
</script>

<style>
.demo-ruleForm {
  margin: 50px auto;
}
</style>

<template>
  <alertdetail-title>
    <div slot="leftpannel_title">IVR Messaging | {{ alertID }}</div>
    <div slot="right-pannel" />
    <div slot="left-pannel">
      <el-form ref="ruleForm" :model="ruleForm" :rules="rules">
        <div class="div-content-container">
          <el-row class="div-content-title">
            <el-form-item prop="mailTitle">
              <el-input v-model="ruleForm.mailTitle" type="textarea" :autosize="{ minRows: 2}" placeholder="please input content" />
            </el-form-item>
          </el-row>
          <el-row class="div-content-content">
            <el-form-item prop="mailContent">
              <el-input v-model="ruleForm.mailContent" type="textarea" :autosize="{ minRows: 4}" placeholder="please input content" />
            </el-form-item>
          </el-row>
        </div>
        <div class="div-submit">
          <el-form-item>
            <div class="btncenteralign"> <el-button type="primary" @click="submitForm('ruleForm')">submit</el-button></div>
          </el-form-item>
        </div>
      </el-form>
    </div>
  </alertdetail-title>
</template>

<script>
import AlertdetailTitle from './components/alertdetailTitle'

// eslint-disable-next-line no-unused-vars
const alertID = ''

export default {
  name: 'DetailIVR',
  components: {
    AlertdetailTitle
  },
  data() {
    return {
      ruleForm: {
        mailTitle: 'Editable list Inquiry Form Recipients that prepopulates with the Sites distributions list.',
        mailContent: 'The text body of the email to be sent that informs the Sites of the status change (opposite of the current state), the message content being turned on/off, and any other details deemed necessary.'
      },
      rules: {
        mailTitle: [
          { required: true, message: 'please input content', trigger: 'blur' }
        ],
        mailContent: [
          { required: true, message: 'please input content', trigger: 'blur' }
        ]
      }
    }
  },
  created() {
    const id = this.$route.params && this.$route.params.alertId
    console.log(id)
    this.alertID = id
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$router.push('/alert/detail/' + this.alertID)
          this.$message({
            message: this.$t('i18nView.submitSuccess'),
            type: 'success'
          })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.btncenteralign{
  margin-top:20px;
text-align: center;
}
.el-row {
  height: 60px;
}
.div-content-container{
  // min-height: calc(100vh - 84px);
  min-height: calc(100vh - 260px);
  border: 1px solid  #A5C2E6;
}
.div-content-title{
  border: 1px 1px 0px 0px solid  #A5C2E6;
  margin-bottom: 20px;
}
.div-content-content{
  border: 1px 1px 0px 0px solid  #A5C2E6;
}
</style>

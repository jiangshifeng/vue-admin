<template>
  <div>
    <Form
      :model="form.commitData"
      :label-width="form.formData.labelWidth"
      :inline="form.formData.formInline"
      :rules="form.rules"
      id="common_form">
      <template v-for="item in form.formData.show">
        <!--输入框,type决定类型-->
        <FormItem :label="item.label"
                  v-if="item.component==='input'">
          <Input v-model="form.commitData[item.model]"
                 :placeholder="item.placeholder"
                 :type="item.type"
                 style="width: 150px"
                 @on-blur="emptyCheck(form.commitData[item.model])"/>
        </FormItem>

        <!--电话输入框,正则表达式校验-->
        <FormItem :label="item.label"
                  v-if="item.component==='phone_input'">
          <Input v-model="form.commitData[item.model]"
                 :placeholder="item.placeholder"
                 :type="item.type"
                 style="width: 150px"
                 @on-blur="phoneCheck(form.commitData[item.model])"/>
        </FormItem>

        <!--数字输入-->
        <FormItem :label="item.label"
                  v-if="item.component==='number_input'">
          <InputNumber :max="100" :min="0" v-model="form.commitData[item.model]"></InputNumber>
        </FormItem>

        <!--普通下拉选择,不考虑多选->界面不友好-->
        <FormItem :label="item.label"
                  v-if="item.component==='normal_select'">
          <Select
            :multiple="item.multiple"
            v-model="form.commitData[item.model]"
            style="width:120px"
            :placeholder="item.placeholder"
            clearable >
            <Option
              v-for="item in item.choiceList"
              :value="item.value"
              :key="item.value">{{ item.label }}</Option>
          </Select>
        </FormItem>

        <!--日期选择器,type决定是否为范围还是单日期选择,范围选择器绑定数组-->
        <FormItem :label="item.label"
                  v-if="item.component==='time_select'">
          <DatePicker :type="item.type"
                      :placeholder="item.placeholder"
                      style="width: 205px"
                      v-model="form.commitData[item.model]"
                      placement="bottom"
                      format="yy年MM月dd日"></DatePicker>
        </FormItem>

        <!--地区级联选择器-->
        <FormItem :label="item.label" v-if="item.component==='zone'">
          <div class="flex-row">
            <Cascader :data="zone" v-model="form.commitData[item.model_one]" placeholder="选择地区" style="width: 200px"></Cascader>
            <Input v-model="form.commitData[item.model_two]"
                   placeholder="请输入详细地址"
                   type="text"
                   style="width: 300px"/>
          </div>
        </FormItem>

        <!--提交按钮-->
        <FormItem v-if="item.component==='submit'">
          <Button type="primary" @click="submit">搜索</Button>
        </FormItem>

        <!--登录按钮-->
        <div class="flex-center" v-if="item.conponent==='login_button'" style="margin: 10px 0">
          <Button type="primary" @click="login">{{item.text}}</Button>
        </div>

        <!--出弹框按钮-->
        <FormItem v-if="item.component==='new'">
          <Button type="primary" @click="formModalShow=true">新建</Button>
          <form-modal :show="formModalShow" :form="item.form" @on-cancel="closeEditInfo"></form-modal>
        </FormItem>
      </template>
    </Form>
  </div>

</template>

<script>
  import formModal from '@/components/form_modal'
  import closeModal from '@/mixins/closeModal'
  import zone from '@/assets/zone.js'

  export default {
        name: "normal_form",
        props:['form'],
        mixins:[closeModal],
        data(){
          return{
            formModalShow:false,
            zone
          }
      },
        methods:{
           login(){
             this.$router.push({path:"index"});
           },
          submit(){
            this.$Message.success('正在提交搜索');
          },
          phoneCheck(val){
            if (!(/^[1][3,4,5,7,8][0-9]{9}$/.test(val))) {
              this.$Notice.open({
                title:"手机号码格式错误",
                duration:2
              })
            }
          },
          emptyCheck(val){
            if(val===""){
              this.$Notice.open({
                title:"格式不能为空",
                duration:2
              })
            }
          },
          closeEditInfo(){
             this.formModalShow=false
          }
        },
      components:{
        formModal
      }
    }
</script>

<style scoped lang="less">
  #common_form{
    .ivu-form-item{
      margin-top: 10px;
      margin-bottom: 10px;
    }
    .ivu-form-item-content{
      display: flex;
      flex-direction: row;
    }
  }
</style>
<style lang="less">
  #common_form{
    .ivu-form-item-content{
      display: flex;
      flex-direction: row;
    }
  }
</style>

<template>
  <div>
    <Card style="margin: 15px">
      <normal-form :form="form"></normal-form>
    </Card>
    <Card style="margin: 15px">
      <normal-table :table="tableData"></normal-table>
    </Card>
  </div>
</template>

<script>
  import normalForm from '@/components/normal_form'
  import normalTable from '@/components/normal_table'

  export default {
    name: "property-arrearge",
    data(){
      return{
        form: {
          commitData: {
            boss:"",
            sort:"",
            money:"",
            date:[]
          },
          formData: {
            formInline: true,
            show: [
              {
                component: "input",
                label: "欠费店主",
                model: "boss",
                placeholder: "请输入店主名字",
                type: "text",
              },
              {
                component: "normal_select",
                label: "欠费类别",
                model: "sort",
                placeholder: "请选择类别",
                choiceList: [
                  {label: "电费", value: "电费"},
                  {label: "水费", value: "水费"},
                  {label: "清洁费", value: "清洁费"},
                  {label: "安保费", value: "安保费"},
                  {label: "店铺租金", value: "店铺租金"}
                ]
              },
              {
                component: "normal_select",
                label: "欠费金额",
                model: "money",
                placeholder: "请选择范围",
                choiceList: [
                  {label: "0-500", value: "0-500"},
                  {label: "501-1000", value: "501-1000"},
                  {label: "1001-1500", value: "1001-1500"},
                  {label: "1501-2000", value: "1501-2000"},
                  {label: "2000以上", value: "2000以上"}
                ]
              },
              {
                component: "time_select",
                label: "欠费日期",
                type: "daterange",
                model: "date",
                placeholder: "请选择收费日期",
              },
              {
                component: "submit"
              },
              {
                component:"new",
                form: {
                  commitData: {
                    boss:"",
                    sort:"",
                    money:"",
                    date:[]
                  },
                  formData: {
                    formInline: false,
                    labelWidth:80,
                    show: [
                      {
                        component: "input",
                        label: "欠费店主",
                        model: "boss",
                        placeholder: "请输入店主名字",
                        type: "text",
                      },
                      {
                        component: "input",
                        label: "欠费金额",
                        model: "money",
                        placeholder: "请输入收费金额",
                        type: "text",
                      },
                      {
                        component: "normal_select",
                        label: "欠费类别",
                        model: "sort",
                        placeholder: "请选择类别",
                        choiceList: [
                          {label: "电费", value: "电费"},
                          {label: "水费", value: "水费"},
                          {label: "清洁费", value: "清洁费"},
                          {label: "安保费", value: "安保费"},
                          {label: "店铺租金", value: "店铺租金"}
                        ]
                      },
                      {
                        component: "time_select",
                        label: "欠费日期",
                        type: "daterange",
                        model: "date",
                        placeholder: "请选择收费日期",
                      },
                      {
                        component: "edit"
                      }
                    ]
                  }
                }
              }
            ]
          }
        },
        tableData: {
          head: [
            {
              title:"欠费店主",
              key:"boss"
            },
            {
              title: '欠费类别',
              key: 'sort'
            },
            {
              title: '欠费金额',
              key: 'money'
            },
            {
              title: '欠费日期范围',
              key: 'date'
            },
            {
              title:"操作",
              key: "action",
              width:150,
              render: (h, params) => {
                return h('div', [
                  h('Button', {
                    props: {
                      type: 'primary',
                      size: 'small'
                    },
                    style: {
                      marginRight: '5px'
                    },
                    on: {
                      click: () => {
                        console.log(params);
                        this.tableData.data.splice(params.index,1)
                      }
                    }
                  }, '已收费')
                ])
              }
            }
          ],
          data: [
            {
              boss:"李云龙",
              sort: "安保费",
              money:"388",
              date:"2018年01月01日-2018年02月01日"
            },
            {
              boss:"李云龙",
              sort: "安保费",
              money:"388",
              date:"2018年01月01日-2018年02月01日"
            },
            {
              boss:"李云龙",
              sort: "安保费",
              money:"388",
              date:"2018年01月01日-2018年02月01日"
            },
            {
              boss:"李云龙",
              sort: "安保费",
              money:"388",
              date:"2018年01月01日-2018年02月01日"
            },
            {
              boss:"李云龙",
              sort: "安保费",
              money:"388",
              date:"2018年01月01日-2018年02月01日"
            },
            {
              boss:"李云龙",
              sort: "安保费",
              money:"388",
              date:"2018年01月01日-2018年02月01日"
            }
          ]
        }
      }
    },
    components:{
      normalForm,normalTable
    }
  }
</script>

<style scoped>

</style>

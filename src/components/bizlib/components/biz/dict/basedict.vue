<!--
描述：我的首页-数据字典组件
开发人：sunlf
开发日期：2017年8月17日
-->

<template lang="pug">
  keep-alive
    kalix-table(v-bind:bizKey="bizKey" title='字典列表' v-bind:tableFields="tableFields" v-bind:targetURL="targetURL"
    v-bind:bizDialog="bizDialog" bizSearch="basedictSearch" v-bind:btnList="btnList" v-bind:dialogOptions="dialogOptions")
</template>

<script type="text/ecmascript-6">
  // import BaseTable from '@/components/custom/baseTable'
  // import Vue from 'vue'
  // import {ToolButtonList} from 'config/global.toml'
  // import {registerComponent} from '@/api/register'

  export default {
    name: 'kalix-base-dict',
    props: {
      dialogOptions: {},
      targetURL: String,
      bizDialog: Array,
      bizKey: String,
      dictComponent: Array
    },
    data() {
      return {
        // btnList: ToolButtonList,
        btnList: this.$KalixGlobalConfig.ToolButtonList,
        tableFields: [
          {prop: 'type', label: '类型'},
          {prop: 'label', label: '签名'},
          {prop: 'value', label: '数值'},
          {prop: 'description', label: '备注'},
          {prop: 'createBy', label: '创建人'},
          {prop: 'creationDate', label: '创建日期'}
        ]
      }
    },
    created() {
    },
    methods: {
      regGlobalComponent() {
        // 注册全局组件
        // registerComponent(this.dictComponent)
      }
    },
    components: {
      // BaseTable
    }
  }
</script>

<style scoped lang="stylus">

</style>

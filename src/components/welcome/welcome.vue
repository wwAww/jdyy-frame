<template lang="pug">
  div.welcome
    div Welcome
      b {{name}}
</template>
<script type="text/ecmascript-6">
  import Cache from '../corelib/common/cache'

  export default {
    name: 'Welcome',
    data() {
      return {
        name: null,
        chooseDate: '', // 定义今日数据指标时间插件时间
        items: [] // 定义今日数据指标数据集合
      }
    },
    mounted() {
      this.fetchData()
      this.getDate() // 获取系统当前日期方法
    },
    watch: {'$route': 'fetchData'},
    methods: {
      fetchData() {
        if (this.$route.name === 'login' || this.$route.name === 'workflow') {
          return
        }
        this.name = this.$route.params.app || this.name
        this.getDict()
        // console.log(this.$route.params.name);
      },
      getDict() {
        if (this.name) {
          const DictURL = `/camel/rest/${this.name}/dicts`
          const DictKey = `${this.name.toUpperCase()}-DICT-KEY`
          if (!Cache.get(DictKey)) {
            const data = {
              page: 1,
              start: 0,
              limit: 200,
              sort: '[{\'property\': \'value\', \'direction\': \'ASC\'}]'
            }
            this.axios.get(DictURL, {
              params: data
            }).then(response => {
              if (response.data) {
                Cache.save(DictKey, JSON.stringify(response.data.data))
                console.log(`dict cached under key ${DictKey}`, response.data)
              }
            })
          }
        }
      }
    },
    components: {},
    computed: {}
  }
</script>
<style scoped lang="stylus" type="text/stylus">
</style>

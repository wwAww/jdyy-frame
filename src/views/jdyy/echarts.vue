<template lang="pug">
  div.start
    div.left
      div.left_box
        div.left_line
          div.text_box.text 今日数据指标
          div.left_sx
          div.left_zx
          div.left_xx
          div.left_xr
          input.input_time(v-model="datevalue1"  type="date" )
          div.left_block
            ul(v-for="item in items")
              li.block_box
                span.block_span 原住院人数
                span.block_spantwo {{item.a}}
              li.block_box
                span.block_span 出院人数
                span.block_spantwo {{item.b}}
              li.block_box
                span.block_span 入院（转）入人数
                span.block_spantwo {{item.c}}
              li.block_box
                span.block_span 手术人数
                span.block_spantwo {{item.d}}
              li.block_box
                span.block_span 死亡人数
                span.block_spantwo {{item.e}}
              li.block_box
                span.block_span 现住院人数
                span.block_spantwo {{item.f}}
              li.block_box
                span.block_span 重病人数
                span.block_spantwo {{item.g}}
      div.lefttwo
        div.left_box
          div.left_line
            div.text_box.text 月份数据获取
            div.left_sx
            div.left_zx
            div.left_xx
            div.left_xr
            input.input_time(v-model="datevalue2"  type="date" )
            div( id="zhuzhuang" style="width: 90%;height: 300px;left:5%;")
    div.right
      div.left_box
        div.left_line
          div.text_box.text 术式分析
          div.left_sx
          div.left_zx
          div.left_xx
          div.left_xr
          div.block
            input.input_time(v-model="datevalue3"  type="date" )
            span  年龄段
            input.block_input
            span ~
            input.block_input
            el-radio(v-model="radio"  label="1") 男
            el-radio(v-model="radio"  label="2") 女
          div(id="main" style="width: 90%;height: 260px;left:5%;")
      div.lefttwo
        div.left_box
          div.left_line
            div.text_box.text 平均住院日走势图
            div.left_sx
            div.left_zx
            div.left_xx
            div.left_xr
            div(id="diagram" style="width: 90%;height: 260px;left:5%;")
      div.lefttwo
        div.left_box
          div.left_line
            div.text_box.text 诊断分析
            div.left_sx
            div.left_zx
            div.left_xx
            div.left_xr
            div.block
              input.input_time(v-model="datevalue4"  type="date" )
              span  年龄段
              input.block_input
              span ~
              input.block_input
              el-radio(v-model="radio"  label="1") 男
              el-radio(v-model="radio"  label="2") 女
            div(id="main1" style="width: 90%;height: 260px;left:5%;")
</template>

<script>
  // 引入基本模板
  let echarts = require('echarts/lib/echarts')
  // 引入柱状图组件
  require('echarts/lib/chart/bar')
  // 引入提示框和title组件
  require('echarts/lib/component/tooltip')
  require('echarts/lib/component/title')
  export default {
    name: '',
    data () {
      return {
        datevalue1: '',
        datevalue2: '',
        datevalue3: '',
        datevalue4: '',
        radio: '',
        charts: '',
        charts2: '',
        charts3: '',
        opinion: ['骨关节置换', 'MR', 'CR', '髋关节置换', 'CS', 'US', 'ES'],
        opinionData: [
          {value: 351, name: '骨关节置换'},
          {value: 139, name: 'MR'},
          {value: 122, name: 'CR'},
          {value: 122, name: '髋关节置换'},
          {value: 58, name: 'CS'},
          {value: 281, name: 'US'},
          {value: 19, name: 'ES'}
        ],
        items: [
          {a: '35', b: '20', c: '15', d: '5', e: '0', f: '10', g: '15'}
        ]
      }
    },
    methods: {
      drawPie (id) {
        this.charts = echarts.init(document.getElementById(id))
        this.charts.setOption({
          tooltip: {
            trigger: 'item',
            formatter: '{a}<br/>{b}:{c} ({d}%)'
          },
          legend: {
            orient: 'vertical',
            x: 'left',
            data: this.opinion,
            textStyle: {
              color: '#ffffff'
            }
          },
          series: [
            {
              name: '',
              type: 'pie',
              radius: '55%',
              center: ['50%', '50%'],
              avoidLabelOverlap: false,
              data: this.opinionData,
              color: ['#f49f42', '#00BFFF', '#FF0000', '#3CB371', '#9370DB', '#808080', '#00FFFF']
            }
          ]
        })
      },
      zhuzhuang(id) {
        this.charts2 = echarts.init(document.getElementById(id))
        this.charts2.setOption({
          tooltip: {
            trigger: 'axis',
            axisPointer: {
              type: 'shadow'
            }
          },
          legend: {
            data: ['手术人数'],
            textStyle: {
              color: '#ffffff'
            }
          },
          grid: {
            left: '3%',
            right: '3%',
            bottom: '2%',
            containLabel: true
          },
          xAxis: [
            {
              type: 'category',
              data: ['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月'],
              axisLabel: {
                show: true,
                textStyle: {
                  color: '#2d8ac7'
                }
              }
            }
          ],
          yAxis: [
            {
              type: 'value',
              axisLabel: {
                show: true,
                textStyle: {
                  color: '#2d8ac7'
                }
              }
            }
          ],
          series: [
            {
              name: '手术人数',
              type: 'bar',
              barWidth: '30%',
              data: [2000, 2500, 1800, 2000, 2500, 1800, 1800, 1500, 1800, 1800, 1500, 500],
              color: '#2d8ac7'
            }
          ]
        })
      },
      diagram (id) {
        this.charts3 = echarts.init(document.getElementById(id))
        this.charts3.setOption({
          tooltip: {
            trigger: 'axis'
          },
          legend: {
            data: ['2018', '2017', '2016', '2015', '2014'],
            textStyle: {
              color: '#2d8ac7'
            }
          },
          grid: {
            left: '3%',
            right: '4%',
            bottom: '3%',
            containLabel: true
          },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: ['', '一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月'],
            axisLabel: {
              show: true,
              textStyle: {
                color: '#2d8ac7'
              }
            }
          },
          yAxis: {
            type: 'value',
            axisLabel: {
              show: true,
              textStyle: {
                color: '#2d8ac7'
              }
            }
          },
          series: [
            {
              name: '2018',
              type: 'line',
              stack: '总量',
              smooth: true,
              data: [210, 132, 101, 134, 90, 230, 210, 120, 132, 101, 134, 90, 230, 210]
            },
            {
              name: '2017',
              type: 'line',
              stack: '总量',
              smooth: true,
              data: [0, 182, 191, 234, 290, 330, 310, 120, 132, 101, 134, 90, 230, 210]
            },
            {
              name: '2016',
              type: 'line',
              stack: '总量',
              smooth: true,
              data: [210, 232, 201, 154, 190, 330, 410, 120, 132, 101, 134, 90, 230, 210]
            },
            {
              name: '2015',
              type: 'line',
              stack: '总量',
              smooth: true,
              data: [210, 332, 301, 334, 390, 330, 320, 120, 132, 101, 134, 90, 230, 210]
            },
            {
              name: '2014',
              type: 'line',
              stack: '总量',
              smooth: true,
              data: [210, 932, 901, 934, 1290, 1330, 1320, 120, 132, 101, 134, 90, 230, 210]
            }
          ]
        })
      }
    },
    // 调用
    mounted () {
      this.$nextTick(function() {
        this.drawPie('main')
        this.zhuzhuang('zhuzhuang')
        this.drawPie('main1')
        this.diagram('diagram')
      })
    }
  }
</script>

<style scoped lang="stylus" type="text/stylus">
  * {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .start
    width 98%
    height 1000px
    padding 40px 10px
    color #2d8ac7
    background-color #02010f
    .left
      width 49%
      float left
      .left_box
          width 98%
          margin auto
          height 440px
          border 2px solid #23769a
        .left_line
            width 98%
            height 420px
            margin 10px auto
            border 0.3px solid #23769a
            border-radius 5px
            box-shadow 0px 0px  10px 5px #23769a inset
          .text_box
              width 30%
              position relative
              background-color rgba(1,14,45,0.8)
              margin -25px 0 0 15%
              text-align center
              font-size 1.2vw
              color #3ac8f3
              font-weight bold
              padding 5px 0
          .left_sx
            width 30px
            height 5px
            background-color #3ac8f3
            position absolute
            margin -23px 0 0 -14px
          .left_zx
            width 5px
            height 30px
            background-color #3ac8f3
            position absolute
            margin -18px 0 0 -14px
          .left_xr
            width 5px
            height 30px
            background-color #3ac8f3
            float right
            margin 398px -33px 0 0
          .left_xx
            width 30px
            height 5px
            background-color #3ac8f3
            float right
            margin 423px -12px 0 0
          .input_time
            width 120px
            margin-top 15px
            margin-left 80%
            border 2px solid #23769a
            color #23769a
            background-color black
          .left_block
            width 90%
            margin auto
            position relative
            margin-top 20px
            height 300px
            .block_box
              width 90%
              height 30px
              line-height 30px
              background-color #373641
              margin  10px auto
              font-size 1vw
              .block_span
                width 90%
                color #23769a
                padding-left 5px
                float left
              .block_spantwo
                  width 8%
                  color #23769a
                  float right
      .lefttwo
        margin-top 120px
    .right
      width 49%
      float right
      .left_box
        width 90%
        margin auto
        height 320px
        border 2px solid #23769a
        .left_line
          width 98%
          height 300px
          margin 10px auto
          border 0.3px solid #23769a
          border-radius 5px
          box-shadow 0px 0px  10px 5px #23769a inset
          .text_box
            width 30%
            position relative
            background-color rgba(1,14,45,0.8)
            margin -25px 0 0 15%
            text-align center
            font-size 1.2vw
            color #3ac8f3
            font-weight bold
            padding 5px 0
          .left_sx
            width 30px
            height 5px
            background-color #3ac8f3
            position absolute
            margin -22px 0 0 -12px
          .left_zx
            width 5px
            height 30px
            background-color #3ac8f3
            position absolute
            margin -18px 0 0 -12px
          .left_xr
            width 5px
            height 30px
            background-color #3ac8f3
            float right
            margin 278px -31px 0 0
          .left_xx
            width 30px
            height 5px
            background-color #3ac8f3
            float right
            margin 304px -12px 0 0
          .block
            margin-left 30%
            width 70%
          .input_time
            width 120px
            margin-top 15px
            border 2px solid #23769a
            color #23769a
            background-color black
          .block_input
            width 60px
            margin-top 15px
            border 2px solid #23769a
            color #23769a
            background-color black
          .el-radio
            color: #23769a ;
            font-weight: 500;
            line-height: 1;
            cursor: pointer;
            white-space: nowrap;
            outline: 0
            margin-left 2%
            background-color black
      .lefttwo
        margin-top 20px
</style>

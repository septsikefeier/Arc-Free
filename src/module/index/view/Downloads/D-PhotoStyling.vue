<template>
  <div id="D-PhotoStyling">
    <div class="border-top">
      <LineChartHeader @transferTimeRangeValue="acceptTimeRangeValue">
        <span slot="titleSlot">整体趋势</span>
      </LineChartHeader>
      <div class="tab-charts">
        <el-tabs v-model="activeName" @tab-click ="tabChart">
          <el-tab-pane label="新增下载量" name="1">
            <div class="containers">
              <LineChart ref ="line1"
                         :time-axis = "timeSlotArr"
                         :lines ="lines"
                         :title = "title"
                         chart-id="a"
              ></LineChart>
            </div>
          </el-tab-pane>
          <el-tab-pane label="累计下载量" name="2">
            <div class="containers">
              <LineChart ref ="line2"
                         :time-axis = "timeSlotArr"
                         :lines ="lines"
                         :title = "title2"
                         chart-id="b"
                         :is-stacked="true"
              ></LineChart>
            </div>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
  </div>
</template>
<script>
  import LineChartHeader from '../../../.././components/lineChartHeader'
  import LineChart from '../../../.././components/charts/lineChart'
  export default {
    data() {
      return {
        activeName: '1',
        timeRangeValue: 2,
        lines : [{
          name:"ArcFace",data:[12,21,23,44,17,21,12]
        },{
          name:"PhotoStyling",data:[2,3,4,5,6,7,6]
        }],
        title : '普通折线图',
        title2 : '堆积折线图',
        timeSlotArr: ['2017-1-2','2017-1-3','2017-1-4','2017-1-5','2017-1-6','2017-1-7',
          '2017-1-8'],
      }
    },
    watch: {
      timeRangeValue(val) {
        console.log('123')
      }
    },
    components: {
      LineChartHeader,
      LineChart
    },
    methods: {
      acceptTimeRangeValue(timeRangValue) {
        this.timeRangeValue = timeRangValue
        console.log(this.timeRangeValue)
      },
      tabChart(){
        if (this.activeName === '2') {
          this.$nextTick(() => {
            this.$refs.line2.drawLine()
          })
        }
      }
    },
    mounted() {
      this.$nextTick(() => {
        this.$refs.line1.drawLine()
      })
    },
    created() {
    /*  this.$API.GetDownloadsPS({
       timeRangeValue: this.timeRangeValue
       }).then(function (data) {
       console.log('成功')
       }).catch(function (error) {
       console.log('失败')
       })*/
    }
  }
</script>
<style lang="scss">
  #D-PhotoStyling {
    .down-select {
      display: none;
    }
    .el-tabs__active-bar {
      background-color: #13CE66;
      height: 2px;
    }
    .el-tabs__item.is-active {
      color: #13CE66;
    }
    .containers {
      width: 100%;
      height: 400px;
    }
  }
</style>

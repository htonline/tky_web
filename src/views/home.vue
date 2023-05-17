<template>
  <div class="dashboard-container">
    <div class="dashboard-editor-container">
      <div class="card-panel-text">
        <span>检测单位信息</span>
        <el-row :gutter="40" class="panel-group">
          <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
            <div class="card-panel" @click="handleSetLineChartData('messages')">
              <div class="card-panel-icon-wrapper icon-message">
                <!-- 放图标 -->
                <svg-icon icon-class="user" class-name="card-panel-icon" />
              </div>
              <div class="card-panel-description">
                <div class="card-panel-text">
                  检测单位
                </div>
                <count-to :start-val="0" :end-val="th2" :duration="3000" class="card-panel-num" />
              </div>
            </div>
          </el-col>
          <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
            <div class="card-panel" @click="handleSetLineChartData('messages')">
              <div class="card-panel-icon-wrapper icon-message">
                <svg-icon icon-class="qiniu" class-name="card-panel-icon" />
              </div>
              <div class="card-panel-description">
                <div class="card-panel-text">
                  线路名称
                </div>
                <count-to :start-val="0" :end-val="th2" :duration="3000" class="card-panel-num" />
              </div>
            </div>
          </el-col>
          <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
            <div class="card-panel" @click="handleSetLineChartData('messages')">
              <div class="card-panel-icon-wrapper icon-message">
                <svg-icon icon-class="sys-tools" class-name="card-panel-icon" />
              </div>
              <div class="card-panel-description">
                <div class="card-panel-text">
                  隧道的检测方案
                </div>
                <count-to :start-val="0" :end-val="th2" :duration="3000" class="card-panel-num" />
              </div>
            </div>
          </el-col>
        </el-row>
      </div>
      <!-- <github-corner class="github-corner" /> -->
      <div class="card-panel-text">
        <span>衬砌检测总体概况</span>
        <panel-group @handleSetLineChartData="handleSetLineChartData" />
      </div>
      <el-row :gutter="32">
        <!--
        <el-col :xs="24" :sm="24" :lg="8">
          <div class="chart-wrapper">
            <radar-chart />
          </div>
        </el-col>
        -->
        <el-col :xs="8" :sm="8" :lg="6">
          <div class="chart-wrapper">
            <pie-chart2 />
          </div>
        </el-col>
        <el-col :xs="8" :sm="8" :lg="6">
          <div class="chart-wrapper">
            <pie-chart3 />
          </div>
        </el-col>
        <el-col :xs="24" :sm="24" :lg="6">
          <div class="chart-wrapper">
            <bar-chart1 />
          </div>
        </el-col>
        <el-col :xs="24" :sm="24" :lg="6">
          <div class="chart-wrapper">
            <bar-chart2 />
          </div>
        </el-col>
      </el-row>
      <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
        <!-- <line-chart :chart-data="lineChartData" />  -->
        <line-chart />
      </el-row>
    </div>
  </div>
</template>

<script>
import PanelGroup from './dashboard/PanelGroup1'
import LineChart from './dashboard/LineChart1'
import RadarChart from '@/components/Echarts/RadarChart'
import PieChart2 from '@/components/Echarts/PieChart2'
import PieChart3 from '@/components/Echarts/PieChart3'
import BarChart1 from '@/components/Echarts/BarChart1'
import BarChart2 from '@/components/Echarts/BarChart2'

const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}

export default {
  name: 'Dashboard',
  components: {
    // GithubCorner,
    PanelGroup,
    LineChart,
    RadarChart,
    PieChart2,
    PieChart3,
    BarChart1,
    BarChart2
  },
  data() {
    return {
      lineChartData: lineChartData.newVisitis
    }
  },
  methods: {
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type]
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .dashboard-editor-container {
    padding: 32px;
    background-color: rgb(240, 242, 245);
    position: relative;
    .chart-wrapper {
      background: #fff;
      padding: 16px 16px 0;
      margin-bottom: 32px;
    }
  }
  .panel-group {
    margin-top: 18px;

    .card-panel-col {
      margin-bottom: 32px;
    }

    .card-panel {
      height: 108px;
      cursor: pointer;
      font-size: 12px;
      position: relative;
      overflow: hidden;
      color: #666;
      background: #fff;
      box-shadow: 4px 4px 40px rgba(0, 0, 0, .05);
      border-color: rgba(0, 0, 0, .05);

      &:hover {
        .card-panel-icon-wrapper {
          color: #fff;
        }

        .icon-people {
          background: #40c9c6;
        }

        .icon-message {
          background: #36a3f7;
        }

        .icon-money {
          background: #f4516c;
        }

        .icon-shopping {
          background: #34bfa3
        }
      }

      .icon-people {
        color: #40c9c6;
      }

      .icon-message {
        color: #36a3f7;
      }

      .icon-money {
        color: #f4516c;
      }

      .icon-shopping {
        color: #34bfa3
      }

      .card-panel-icon-wrapper {
        float: left;
        margin: 14px 0 0 14px;
        padding: 16px;
        transition: all 0.38s ease-out;
        border-radius: 6px;
      }

      .card-panel-icon {
        float: left;
        font-size: 48px;
      }

      .card-panel-description {
        float: right;
        font-weight: bold;
        margin: 26px;
        margin-left: 0px;

        .card-panel-text {
          line-height: 18px;
          color: rgba(0, 0, 0, 0.45);
          font-size: 16px;
          margin-bottom: 12px;
        }

        .card-panel-num {
          font-size: 20px;
        }
      }
    }
  }

  @media (max-width:1024px) {
    .chart-wrapper {
      padding: 8px;
    }
    .card-panel-description {
      display: none;
    }

    .card-panel-icon-wrapper {
      float: none !important;
      width: 100%;
      height: 100%;
      margin: 0 !important;

      .svg-icon {
        display: block;
        margin: 14px auto !important;
        float: none !important;
      }
    }
  }
</style>

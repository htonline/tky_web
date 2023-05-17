<!--首页板块-->
<template>
  <el-row :gutter="40" class="panel-group">

    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('shoppings')">
        <div class="card-panel-icon-wrapper icon-shopping">
          <svg-icon icon-class="tunnel" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            隧道信息（座）
          </div>
          <count-to :start-val="0" :end-val="th1" :duration="2000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('messages')">
        <div class="card-panel-icon-wrapper icon-message">
          <svg-icon icon-class="lineLength" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            隧道总长度（米）
          </div>
          <count-to :start-val="0" :end-val="th2" :duration="3000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <!--    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">-->
    <!--      <div class="card-panel" @click="handleSetLineChartData('newVisitis')">-->
    <!--        <div class="card-panel-icon-wrapper icon-people">-->
    <!--          <svg-icon icon-class="work" class-name="card-panel-icon" />-->
    <!--        </div>-->
    <!--        <div class="card-panel-description">-->
    <!--          <div class="card-panel-text">-->
    <!--            已施工进度（米）-->
    <!--          </div>-->
    <!--          <count-to :start-val="0" :end-val="th3" :duration="2600" class="card-panel-num" />-->
    <!--        </div>-->
    <!--      </div>-->
    <!--    </el-col>-->
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('messages')">
        <div class="card-panel-icon-wrapper icon-message">
          <svg-icon icon-class="baojiandan" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            已报检总长度（米）
          </div>
          <count-to :start-val="0" :end-val="th4" :duration="3000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('messages')">
        <div class="card-panel-icon-wrapper icon-message">
          <svg-icon icon-class="jindutiao" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            已检测进度（米）
          </div>
          <count-to :start-val="0" :end-val="th5" :duration="3000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('shoppings')">
        <div class="card-panel-icon-wrapper icon-shopping">
          <svg-icon icon-class="finsh" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            已处置缺陷（个）
          </div>
          <count-to :start-val="0" :end-val="th6" :duration="3600" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('purchases')">
        <div class="card-panel-icon-wrapper icon-money">
          <svg-icon icon-class="unfinsh" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            缺陷数量（个）
          </div>
          <count-to :start-val="0" :end-val="th7" :duration="3200" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('shoppings')">
        <div class="card-panel-icon-wrapper icon-shopping">
          <svg-icon icon-class="jiancelv" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            检测进度
          </div>
          <count-to :start-val="0" :end-val="th8" :duration="3600" class="card-panel-num" />%
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<script>
import CountTo from 'vue-count-to'
import { selectParam } from '@/api/system/tunnelInformation'

export default {
  components: {
    CountTo
  },
  data() {
    return {
      th1: 0,
      th2: 0,
      th3: 0,
      th4: 0,
      th5: 0,
      th6: 0,
      th7: 0,
      th8: 0
    }
  },
  mounted: function() {
    selectParam().then(response => {
      console.log('response', response)
      this.th1 = response.tunnelNumner
      this.th2 = response.tunnelLength
      this.th3 = response.finishlength
      this.th4 = response.baojiandanLength
      this.th5 = response.yijianceLength
      this.th6 = response.yichuliquexian
      this.th7 = response.weichuliquexian
      this.th8 = response.jiancelv
      // this.$confirm(response)
    })
  },
  methods: {
    handleSetLineChartData(type) {
      this.$emit('handleSetLineChartData', type)
    }
  }
}
</script>

<style lang="scss" scoped>
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

@media (max-width:550px) {
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

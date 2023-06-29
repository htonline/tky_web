<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <label class="el-form-item-label">雷达id</label>
        <el-input v-model="query.radarId" clearable placeholder="雷达id" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">雷达文件名称</label>
        <el-input v-model="query.radarName" clearable placeholder="雷达文件名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">来源公司id</label>
        <el-input v-model="query.companyId" clearable placeholder="来源公司id" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
<!--        <label class="el-form-item-label">经纬度坐标</label>-->
<!--        <el-input v-model="query.longLat" clearable placeholder="经纬度坐标" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
        <label class="el-form-item-label">道路名称</label>
        <el-input v-model="query.roadName" clearable placeholder="道路名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">雷达型号</label>
        <el-input v-model="query.radarType" clearable placeholder="雷达型号" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">天线主频</label>
        <el-input v-model="query.basicFrequency" clearable placeholder="天线主频" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">时间窗</label>
        <el-input v-model="query.timeWindow" clearable placeholder="时间窗" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">采样间隔</label>
        <el-input v-model="query.samplingInterval" clearable placeholder="采样间隔" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">测量宽度</label>
        <el-input v-model="query.measuringWidth" clearable placeholder="测量宽度" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
<!--        <label class="el-form-item-label">数据大小</label>-->
<!--        <el-input v-model="query.dataSize" clearable placeholder="数据大小" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
        <label class="el-form-item-label">总道数</label>
        <el-input v-model="query.traceNum" clearable placeholder="总道数" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">通道数</label>
        <el-input v-model="query.channel" clearable placeholder="通道数" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">起始里程</label>
        <el-input v-model="query.startMileage" clearable placeholder="起始里程" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">终止里程</label>
        <el-input v-model="query.endMileage" clearable placeholder="终止里程" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
<!--        <label class="el-form-item-label">删除标志</label>-->
<!--        <el-input v-model="query.delFlag" clearable placeholder="删除标志" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">原始雷达数据存放地址</label>-->
<!--        <el-input v-model="query.radAdd" clearable placeholder="原始雷达数据存放地址" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Gps文件存放地址</label>-->
<!--        <el-input v-model="query.gpsAdd" clearable placeholder="Gps文件存放地址" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">解析后雷达数据存放地址</label>-->
<!--        <el-input v-model="query.anaAdd" clearable placeholder="解析后雷达数据存放地址" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">雷达图片存放地址</label>-->
<!--        <el-input v-model="query.picAdd" clearable placeholder="雷达图片存放地址" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">创建者</label>-->
<!--        <el-input v-model="query.createBy" clearable placeholder="创建者" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">更新者</label>-->
<!--        <el-input v-model="query.updateBy" clearable placeholder="更新者" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark1" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark2" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark3" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark4" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark5" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注</label>-->
<!--        <el-input v-model="query.remark6" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
        <rrOperation :crud="crud" />
      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="雷达id" prop="radarId">
            <el-input v-model="form.radarId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="雷达文件名称">
            <el-input v-model="form.radarName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="来源公司id">
            <el-input v-model="form.companyId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="经纬度坐标">
            <el-input v-model="form.longLat" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="来源城市">
            <el-input v-model="form.cityName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="道路名称">
            <el-input v-model="form.roadName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="雷达型号">
            <el-input v-model="form.radarType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="天线主频">
            <el-input v-model="form.basicFrequency" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="时间窗">
            <el-input v-model="form.timeWindow" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="采样间隔">
            <el-input v-model="form.samplingInterval" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="测量宽度">
            <el-input v-model="form.measuringWidth" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="数据大小">
            <el-input v-model="form.dataSize" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="总道数">
            <el-input v-model="form.traceNum" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="通道数">
            <el-input v-model="form.channel" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="起始里程">
            <el-input v-model="form.startMileage" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="终止里程">
            <el-input v-model="form.endMileage" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="删除标志">
            <el-input v-model="form.delFlag" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="原始雷达数据存放地址">
            <el-input v-model="form.radAdd" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Gps文件存放地址">
            <el-input v-model="form.gpsAdd" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="解析后雷达数据存放地址">
            <el-input v-model="form.anaAdd" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="雷达图片存放地址">
            <el-input v-model="form.picAdd" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="创建者">
            <el-input v-model="form.createBy" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="创建时间">
            <el-input v-model="form.createTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="更新者">
            <el-input v-model="form.updateBy" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="更新时间">
            <el-input v-model="form.updateTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark1" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark2" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark3" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark4" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark5" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark6" style="width: 370px;" />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="text" @click="crud.cancelCU">取消</el-button>
          <el-button :loading="crud.status.cu === 2" type="primary" @click="crud.submitCU">确认</el-button>
        </div>
      </el-dialog>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="crud.data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column type="selection" width="55" />
        <el-table-column prop="radarId" label="雷达id" />
        <el-table-column prop="radarName" label="雷达文件名称" />
        <el-table-column prop="companyId" label="来源公司id" />
        <el-table-column prop="longLat" label="经纬度坐标" />
        <el-table-column prop="cityName" label="来源城市" />
        <el-table-column prop="roadName" label="道路名称" />
        <el-table-column prop="radarType" label="雷达型号" />
        <el-table-column prop="basicFrequency" label="天线主频" />
        <el-table-column prop="timeWindow" label="时间窗" />
        <el-table-column prop="samplingInterval" label="采样间隔" />
        <el-table-column prop="measuringWidth" label="测量宽度" />
        <el-table-column prop="dataSize" label="数据大小" />
        <el-table-column prop="traceNum" label="总道数" />
        <el-table-column prop="channel" label="通道数" />
        <el-table-column prop="startMileage" label="起始里程" />
        <el-table-column prop="endMileage" label="终止里程" />
        <el-table-column prop="delFlag" label="删除标志" />
        <el-table-column prop="radAdd" label="原始雷达数据存放地址" />
        <el-table-column prop="gpsAdd" label="Gps文件存放地址" />
        <el-table-column prop="anaAdd" label="解析后雷达数据存放地址" />
        <el-table-column prop="picAdd" label="雷达图片存放地址" />
        <el-table-column prop="createBy" label="创建者" />
        <el-table-column prop="createTime" label="创建时间" />
        <el-table-column prop="updateBy" label="更新者" />
        <el-table-column prop="updateTime" label="更新时间" />
        <el-table-column prop="remark" label="备注" />
        <el-table-column prop="remark1" label="备注" />
        <el-table-column prop="remark2" label="备注" />
        <el-table-column prop="remark3" label="备注" />
        <el-table-column prop="remark4" label="备注" />
        <el-table-column prop="remark5" label="备注" />
        <el-table-column prop="remark6" label="备注" />
        <el-table-column v-if="checkPer(['admin','radar:edit','radar:del'])" label="操作" width="150px" align="center">
          <template slot-scope="scope">
            <udOperation
              :data="scope.row"
              :permission="permission"
            />
          </template>
        </el-table-column>
      </el-table>
      <!--分页组件-->
      <pagination />
    </div>
  </div>
</template>

<script>
import crudRadar from '@/api/radar'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

const defaultForm = { radarId: null, radarName: null, companyId: null, longLat: null, cityName: null, roadName: null, radarType: null, basicFrequency: null, timeWindow: null, samplingInterval: null, measuringWidth: null, dataSize: null, traceNum: null, channel: null, startMileage: null, endMileage: null, delFlag: null, radAdd: null, gpsAdd: null, anaAdd: null, picAdd: null, createBy: null, createTime: null, updateBy: null, updateTime: null, remark: null, remark1: null, remark2: null, remark3: null, remark4: null, remark5: null, remark6: null }
export default {
  name: 'Radar',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: 'radar', url: 'api/radar', idField: 'radarId', sort: 'radarId,desc', crudMethod: { ...crudRadar }})
  },
  data() {
    return {
      permission: {
        add: ['admin', 'radar:add'],
        edit: ['admin', 'radar:edit'],
        del: ['admin', 'radar:del']
      },
      rules: {
        radarId: [
          { required: true, message: '雷达id不能为空', trigger: 'blur' }
        ]
      },
      queryTypeOptions: [
        { key: 'radarId', display_name: '雷达id' },
        { key: 'radarName', display_name: '雷达文件名称' },
        { key: 'companyId', display_name: '来源公司id' },
        { key: 'longLat', display_name: '经纬度坐标' },
        { key: 'roadName', display_name: '道路名称' },
        { key: 'radarType', display_name: '雷达型号' },
        { key: 'basicFrequency', display_name: '天线主频' },
        { key: 'timeWindow', display_name: '时间窗' },
        { key: 'samplingInterval', display_name: '采样间隔' },
        { key: 'measuringWidth', display_name: '测量宽度' },
        { key: 'dataSize', display_name: '数据大小' },
        { key: 'traceNum', display_name: '总道数' },
        { key: 'channel', display_name: '通道数' },
        { key: 'startMileage', display_name: '起始里程' },
        { key: 'endMileage', display_name: '终止里程' },
        { key: 'delFlag', display_name: '删除标志' },
        { key: 'radAdd', display_name: '原始雷达数据存放地址' },
        { key: 'gpsAdd', display_name: 'Gps文件存放地址' },
        { key: 'anaAdd', display_name: '解析后雷达数据存放地址' },
        { key: 'picAdd', display_name: '雷达图片存放地址' },
        { key: 'createBy', display_name: '创建者' },
        { key: 'updateBy', display_name: '更新者' },
        { key: 'remark', display_name: '备注' },
        { key: 'remark1', display_name: '备注' },
        { key: 'remark2', display_name: '备注' },
        { key: 'remark3', display_name: '备注' },
        { key: 'remark4', display_name: '备注' },
        { key: 'remark5', display_name: '备注' },
        { key: 'remark6', display_name: '备注' }
      ]
    }
  },
  methods: {
    // 钩子：在获取表格数据之前执行，false 则代表不获取数据
    [CRUD.HOOK.beforeRefresh]() {
      return true
    }
  }
}
</script>

<style scoped>

</style>

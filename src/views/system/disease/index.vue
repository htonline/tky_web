<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <label class="el-form-item-label">病害id</label>
        <el-input v-model="query.diseaseId" clearable placeholder="病害id" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">雷达文件名称</label>
        <el-input v-model="query.radarName" clearable placeholder="雷达文件名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">岩土性质</label>
        <el-input v-model="query.soilProperty" clearable placeholder="岩土性质" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">病害种类</label>
        <el-input v-model="query.diseaseType" clearable placeholder="病害种类" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">起始深度（采样点数）</label>
        <el-input v-model="query.startDepth" clearable placeholder="起始深度（采样点数）" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">终止深度（采样点数）</label>
        <el-input v-model="query.endDepth" clearable placeholder="终止深度（采样点数）" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">净空高</label>
        <el-input v-model="query.freeHeight" clearable placeholder="净空高" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">宽度开始通道数</label>
        <el-input v-model="query.startWidth" clearable placeholder="宽度开始通道数" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">宽度结束通道数</label>
        <el-input v-model="query.endWidth" clearable placeholder="宽度结束通道数" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">尺寸</label>
        <el-input v-model="query.diseaseSize" clearable placeholder="尺寸" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">中心点经纬度坐标</label>
        <el-input v-model="query.longLat" clearable placeholder="中心点经纬度坐标" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">删除标志</label>
        <el-input v-model="query.delFlag" clearable placeholder="删除标志" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">创建者</label>
        <el-input v-model="query.createBy" clearable placeholder="创建者" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">更新者</label>
        <el-input v-model="query.updateBy" clearable placeholder="更新者" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
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
          <el-form-item label="病害id" prop="diseaseId">
            <el-input v-model="form.diseaseId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="雷达文件名称">
            <el-input v-model="form.radarName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="岩土性质">
            <el-input v-model="form.soilProperty" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="病害种类">
            <el-input v-model="form.diseaseType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="起始深度（采样点数）">
            <el-input v-model="form.startDepth" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="终止深度（采样点数）">
            <el-input v-model="form.endDepth" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="净空高">
            <el-input v-model="form.freeHeight" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="宽度开始通道数">
            <el-input v-model="form.startWidth" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="宽度结束通道数">
            <el-input v-model="form.endWidth" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="尺寸">
            <el-input v-model="form.diseaseSize" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="中心点经纬度坐标">
            <el-input v-model="form.longLat" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="删除标志">
            <el-input v-model="form.delFlag" style="width: 370px;" />
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
          <el-form-item label="更新时间">
            <el-input v-model="form.updateTime" style="width: 370px;" />
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
        <el-table-column prop="diseaseId" label="病害id" />
        <el-table-column prop="radarName" label="雷达文件名称" />
        <el-table-column prop="soilProperty" label="岩土性质" />
        <el-table-column prop="diseaseType" label="病害种类" />
        <el-table-column prop="startDepth" label="起始深度（采样点数）" />
        <el-table-column prop="endDepth" label="终止深度（采样点数）" />
        <el-table-column prop="freeHeight" label="净空高" />
        <el-table-column prop="startWidth" label="宽度开始通道数" />
        <el-table-column prop="endWidth" label="宽度结束通道数" />
        <el-table-column prop="diseaseSize" label="尺寸" />
        <el-table-column prop="longLat" label="中心点经纬度坐标" />
        <el-table-column prop="delFlag" label="删除标志" />
        <el-table-column prop="createBy" label="创建者" />
        <el-table-column prop="createTime" label="创建时间" />
        <el-table-column prop="updateBy" label="更新者" />
        <el-table-column prop="remark" label="备注" />
        <el-table-column prop="remark1" label="备注" />
        <el-table-column prop="remark2" label="备注" />
        <el-table-column prop="remark3" label="备注" />
        <el-table-column prop="remark4" label="备注" />
        <el-table-column prop="remark5" label="备注" />
        <el-table-column prop="remark6" label="备注" />
        <el-table-column prop="updateTime" label="更新时间" />
        <el-table-column v-if="checkPer(['admin','disease:edit','disease:del'])" label="操作" width="150px" align="center">
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
import crudDisease from '@/api/disease'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

const defaultForm = { diseaseId: null, radarName: null, soilProperty: null, diseaseType: null, startDepth: null, endDepth: null, freeHeight: null, startWidth: null, endWidth: null, diseaseSize: null, longLat: null, delFlag: null, createBy: null, createTime: null, updateBy: null, remark: null, remark1: null, remark2: null, remark3: null, remark4: null, remark5: null, remark6: null, updateTime: null }
export default {
  name: 'Disease',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: 'disease', url: 'api/disease', idField: 'diseaseId', sort: 'diseaseId,desc', crudMethod: { ...crudDisease }})
  },
  data() {
    return {
      permission: {
        add: ['admin', 'disease:add'],
        edit: ['admin', 'disease:edit'],
        del: ['admin', 'disease:del']
      },
      rules: {
        diseaseId: [
          { required: true, message: '病害id不能为空', trigger: 'blur' }
        ]
      },
      queryTypeOptions: [
        { key: 'diseaseId', display_name: '病害id' },
        { key: 'radarName', display_name: '雷达文件名称' },
        { key: 'soilProperty', display_name: '岩土性质' },
        { key: 'diseaseType', display_name: '病害种类' },
        { key: 'startDepth', display_name: '起始深度（采样点数）' },
        { key: 'endDepth', display_name: '终止深度（采样点数）' },
        { key: 'freeHeight', display_name: '净空高' },
        { key: 'startWidth', display_name: '宽度开始通道数' },
        { key: 'endWidth', display_name: '宽度结束通道数' },
        { key: 'diseaseSize', display_name: '尺寸' },
        { key: 'longLat', display_name: '中心点经纬度坐标' },
        { key: 'delFlag', display_name: '删除标志' },
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

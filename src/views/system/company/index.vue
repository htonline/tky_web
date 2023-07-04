<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <label class="el-form-item-label">公司id</label>
        <el-input v-model="query.companyId" clearable placeholder="公司id" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">公司名称</label>
        <el-input v-model="query.companyName" clearable placeholder="公司名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">联系电话</label>
        <el-input v-model="query.companyPhone" clearable placeholder="联系电话" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">备注</label>
        <el-input v-model="query.remark" clearable placeholder="备注" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
<!--        <label class="el-form-item-label">备注1</label>-->
<!--        <el-input v-model="query.remark1" clearable placeholder="备注1" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注2</label>-->
<!--        <el-input v-model="query.remark2" clearable placeholder="备注2" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注3</label>-->
<!--        <el-input v-model="query.remark3" clearable placeholder="备注3" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注4</label>-->
<!--        <el-input v-model="query.remark4" clearable placeholder="备注4" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注5</label>-->
<!--        <el-input v-model="query.remark5" clearable placeholder="备注5" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">备注6</label>-->
<!--        <el-input v-model="query.remark6" clearable placeholder="备注6" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
        <rrOperation :crud="crud" />
      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="公司id" prop="companyId">
            <el-input v-model="form.companyId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="公司名称">
            <el-input v-model="form.companyName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="联系电话">
            <el-input v-model="form.companyPhone" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注">
            <el-input v-model="form.remark" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注1">
            <el-input v-model="form.remark1" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注2">
            <el-input v-model="form.remark2" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注3">
            <el-input v-model="form.remark3" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注4">
            <el-input v-model="form.remark4" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注5">
            <el-input v-model="form.remark5" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="备注6">
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
        <el-table-column prop="companyId" label="公司id" />
        <el-table-column prop="companyName" label="公司名称" />
        <el-table-column prop="companyPhone" label="联系电话" />
        <el-table-column prop="remark" label="备注" />
        <el-table-column prop="remark1" label="备注1" />
        <el-table-column prop="remark2" label="备注2" />
        <el-table-column prop="remark3" label="备注3" />
        <el-table-column prop="remark4" label="备注4" />
        <el-table-column prop="remark5" label="备注5" />
        <el-table-column prop="remark6" label="备注6" />
        <el-table-column v-if="checkPer(['admin','company:edit','company:del'])" label="操作" width="150px" align="center">
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
import crudCompany from '@/api/company'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

const defaultForm = { companyId: null, companyName: null, companyPhone: null, remark: null, remark1: null, remark2: null, remark3: null, remark4: null, remark5: null, remark6: null }
export default {
  name: 'Company',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: 'company', url: 'api/company', idField: 'companyId', sort: 'companyId,desc', crudMethod: { ...crudCompany }})
  },
  data() {
    return {
      permission: {
        add: ['admin', 'company:add'],
        edit: ['admin', 'company:edit'],
        del: ['admin', 'company:del']
      },
      rules: {
        companyId: [
          { required: true, message: '公司id不能为空', trigger: 'blur' }
        ]
      },
      queryTypeOptions: [
        { key: 'companyId', display_name: '公司id' },
        { key: 'companyName', display_name: '公司名称' },
        { key: 'companyPhone', display_name: '联系电话' },
        { key: 'remark', display_name: '备注' },
        { key: 'remark1', display_name: '备注1' },
        { key: 'remark2', display_name: '备注2' },
        { key: 'remark3', display_name: '备注3' },
        { key: 'remark4', display_name: '备注4' },
        { key: 'remark5', display_name: '备注5' },
        { key: 'remark6', display_name: '备注6' }
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

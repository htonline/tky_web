<template>
  <!--  隧道衬砌信息管理 - 隧道信息管理 -->
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索
        <label class="el-form-item-label">ID</label>
        <el-input v-model="query.tunnelInforId" clearable placeholder="ID" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">项目名称</label>
        <el-input v-model="query.projectName" clearable placeholder="项目名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">标段名称</label>
        <el-input v-model="query.sectionName" clearable placeholder="标段名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">隧道编号</label>
        <el-input v-model="query.tunnelId" clearable placeholder="隧道编号" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">隧道名称</label>
        <el-input v-model="query.tunnelName" clearable placeholder="隧道名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">工点名称</label>
        <el-input v-model="query.worksiteName" clearable placeholder="工点名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">建设单位</label>
        <el-input v-model="query.repairCompany" clearable placeholder="建设单位" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">监理单位</label>
        <el-input v-model="query.supervisionCompany" clearable placeholder="监理单位" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">检测单位</label>
        <el-input v-model="query.detectionCompany" clearable placeholder="检测单位" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">施工单位</label>
        <el-input v-model="query.constructionCompany" clearable placeholder="施工单位" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">用户ID</label>
        <el-input v-model="query.userId" clearable placeholder="用户ID" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">用户名</label>
        <el-input v-model="query.userName" clearable placeholder="用户名" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">用户权限</label>
        <el-input v-model="query.deptId" clearable placeholder="用户权限" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">数据新增时间</label>
        <el-input v-model="query.time" clearable placeholder="数据新增时间" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
       -->
        <label class="el-form-item-label">隧道名称</label>
        <el-input v-model="query.tunnelName" clearable placeholder="隧道名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <rrOperation :crud="crud" />

      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <!--
          <el-form-item label="ID">
            <el-input v-model="form.tunnelInforId" style="width: 370px;" />
          </el-form-item>
          -->
          <el-form-item label="项目名称">
            <el-input v-model="form.projectName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="标段名称">
            <el-input v-model="form.sectionName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="隧道编号">
            <el-input v-model="form.tunnelId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="隧道名称">
            <el-input v-model="form.tunnelName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="工点名称">
            <el-input v-model="form.worksiteName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="隧道起始里程">
            <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="form.beizhu1" style="width: 140px;" /><span> + </span><el-input v-model="form.beizhu5" style="width: 140px;" />
          </el-form-item>
          <el-form-item label="隧道结束里程">
            <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="form.beizhu2" style="width: 140px;" /><span> + </span><el-input v-model="form.beizhu6" style="width: 140px;" />
          </el-form-item>
          <el-form-item label="隧道长度">
            <el-input v-model="form.tunnelLength" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="上传附件材料" enctype="multipart/form-data">
            <el-upload
              ref="upload"
              multiple
              class="upload-demo"
              :action="fileUploadApi + '?name=' + form.name"
              :on-preview="handlePreview"
              :on-remove="handleRemove"
              :auto-upload="false"
              :file-list="fileList"
              :limit="1"
              :before-upload="beforeUpload"
              :headers="headers"
              :on-success="handleSuccess"
              :on-error="handleError"
            >
              <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
              <el-button v-permission="['admin','storage:add']" style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传文件</el-button>
              <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
            </el-upload>
            <el-input ref="inp" v-model="form.beizhu3" style="width: 120px;" type="hidden" @input="changeVersion" />
          </el-form-item>

          <!--
          <el-form-item label="建设单位">
            <el-input v-model="form.repairCompany" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="监理单位">
            <el-input v-model="form.supervisionCompany" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="检测单位">
            <el-input v-model="form.detectionCompany" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="施工单位">
            <el-input v-model="form.constructionCompany" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="用户ID">
            <el-input v-model="form.userId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="用户名">
            <el-input v-model="form.userName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="用户权限">
            <el-input v-model="form.deptId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="数据新增时间">
            <el-input v-model="form.time" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu1">
            <el-input v-model="form.beizhu1" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu2">
            <el-input v-model="form.beizhu2" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu3">
            <el-input v-model="form.beizhu3" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu4">
            <el-input v-model="form.beizhu4" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu5">
            <el-input v-model="form.beizhu5" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu6">
            <el-input v-model="form.beizhu6" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu7">
            <el-input v-model="form.beizhu7" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu8">
            <el-input v-model="form.beizhu8" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu9">
            <el-input v-model="form.beizhu9" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu10">
            <el-input v-model="form.beizhu10" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu11">
            <el-input v-model="form.beizhu11" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu12">
            <el-input v-model="form.beizhu12" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu13">
            <el-input v-model="form.beizhu13" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu14">
            <el-input v-model="form.beizhu14" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="beizhu15">
            <el-input v-model="form.beizhu15" style="width: 370px;" />
          </el-form-item>
          -->
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="text" :before-upload="beforesubmit" @click="crud.cancelCU">取消</el-button>
          <el-button :loading="crud.status.cu === 2" :before-upload="beforesubmit" type="primary" @click="crud.submitCU">确认</el-button>
        </div>
      </el-dialog>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="crud.data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column type="selection" width="55" />
        <el-table-column prop="tunnelInforId" label="序号" />
        <el-table-column prop="projectName" label="项目名称" />
        <el-table-column prop="sectionName" label="标段名称" />
        <el-table-column prop="tunnelId" label="隧道编号" />
        <el-table-column prop="tunnelName" label="隧道名称" />
        <el-table-column prop="worksiteName" label="工点名称" />
        <el-table-column prop="tunnelStartingDistance" label="隧道起始里程" />
        <el-table-column prop="tunnelEndingDistance" label="隧道结束里程" />
        <el-table-column prop="tunnelLength" label="隧道长度" />
        <el-table-column label="附件材料" width="150px" align="center">
          <template slot-scope="scopes">
            <el-button
              class="filter-item"
              size="mini"
              type="info"
              icon="el-icon-search"
              style="color: #f3ecec"
              @click="look(scopes.row)"
            >查看</el-button>
          </template>
        </el-table-column>
        <!--
        <el-table-column prop="repairCompany" label="建设单位" />
        <el-table-column prop="supervisionCompany" label="监理单位" />
        <el-table-column prop="detectionCompany" label="检测单位" />
        <el-table-column prop="constructionCompany" label="施工单位" />
        <el-table-column prop="userId" label="用户ID" />
        <el-table-column prop="userName" label="用户名" />
        <el-table-column prop="deptId" label="用户权限" />
        <el-table-column prop="time" label="数据新增时间" />
        <el-table-column prop="beizhu1" label="beizhu1" />
        <el-table-column prop="beizhu2" label="beizhu2" />
        <el-table-column prop="beizhu3" label="beizhu3" />
        <el-table-column prop="beizhu4" label="beizhu4" />
        <el-table-column prop="beizhu5" label="beizhu5" />
        <el-table-column prop="beizhu6" label="beizhu6" />
        <el-table-column prop="beizhu7" label="beizhu7" />
        <el-table-column prop="beizhu8" label="beizhu8" />
        <el-table-column prop="beizhu9" label="beizhu9" />
        <el-table-column prop="beizhu10" label="beizhu10" />
        <el-table-column prop="beizhu11" label="beizhu11" />
        <el-table-column prop="beizhu12" label="beizhu12" />
        <el-table-column prop="beizhu13" label="beizhu13" />
        <el-table-column prop="beizhu14" label="beizhu14" />
        <el-table-column prop="beizhu15" label="beizhu15" />
        -->
        <el-table-column label="状态" width="170px" align="center" prop="beizhu4">
          <template slot-scope="scope">
            <el-button v-permission="['admin','tunnelInformation:updateStatus']" style="margin-left: 3px" type="text" @click="updateStatus(scope.row,scope.row.beizhu4)">
              {{ scope.row.beizhu4 }}
            </el-button>
          </template>
        </el-table-column>
        <!--
        <el-table-column label="状态" align="center" prop="beizhu4">
          <template slot-scope="scope">
            <el-switch
              v-model=scope.row.beizhu4
              active-color="#409EFF"
              inactive-color="#F56C6C"
              @change="changeEnabled(scope.row)"
            />
          </template>
        </el-table-column>
        -->
        <el-table-column v-if="checkPer(['admin','tunnelInformation:edit','tunnelInformation:del'])" label="操作" width="150px" align="center">
          <template slot-scope="scope">
            <udOperation
              :data="scope.row"
              :permission="permission"
            />
          </template>
        </el-table-column>
      </el-table>
      <el-dialog title="附件材料" :visible.sync="TunnelDialog">
        <el-table ref="table" v-loading="crud.loading" :data="DataList" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
          <el-table-column prop="name" label="文件名">
            <template slot-scope="scope">
              <el-popover
                :content="'点击下载文件'"
                placement="top-start"
                title=""
                width="200"
                trigger="hover"
              >
                <a
                  slot="reference"
                  :href="baseApi + '/file/' + scope.row.type + '/' + scope.row.realName"
                  class="el-link--primary"
                  style="word-break:keep-all;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color: #1890ff;font-size: 13px;"
                  target="_blank"
                >
                  {{ scope.row.realName }}
                </a>
              </el-popover>
            </template>
          </el-table-column>
          <el-table-column prop="path" label="预览图">
            <template slot-scope="{row}">
              <el-image
                :src=" baseApi + '/file/' + row.type + '/' + row.realName"
                :preview-src-list="[baseApi + '/file/' + row.type + '/' + row.realName]"
                fit="contain"
                lazy
                class="el-avatar"
              >
                <div slot="error">
                  <i class="el-icon-document" />
                </div>
              </el-image>
            </template>
          </el-table-column>
          <el-table-column prop="type" label="类别" />
          <el-table-column prop="createTime" label="上传日期" />
        <!--
             <el-table-column  label="操作" >
            <template slot-scope="scope">
              <el-button
                class="filter-item"
                size="mini"
                type="warning"
                icon="el-icon-download"
                @click="download(scope.row)"
              >下载</el-button>
            </template>
        </el-table-column>
        -->
        </el-table>
      </el-dialog>

      <!--分页组件-->
      <pagination />
    </div>
  </div>
</template>

<script>
import crudTunnelInformation from '@/api/system/tunnelInformation'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'
import { mapGetters } from 'vuex'
import { getToken } from '@/utils/auth'
import { select, changeStatue } from '@/api/system/tunnelInformation'

const defaultForm = { tunnelInforId: null, projectName: null, sectionName: null, tunnelId: null, tunnelName: null, worksiteName: null, tunnelStartingDistance: null, tunnelEndingDistance: null, tunnelLength: null, repairCompany: null, supervisionCompany: null, detectionCompany: null, constructionCompany: null, userId: null, userName: null, deptId: null, time: null, beizhu1: null, beizhu2: null, beizhu3: null, beizhu4: null, beizhu5: null, beizhu6: null, beizhu7: null, beizhu8: null, beizhu9: null, beizhu10: null, beizhu11: null, beizhu12: null, beizhu13: null, beizhu14: null, beizhu15: null }
export default {
  name: 'TunnelInformation',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: '隧道信息', url: 'api/tunnelInformation', idField: 'tunnelInforId', sort: 'tunnelInforId,desc', crudMethod: { ...crudTunnelInformation }})
  },
  data() {
    return {
      values: true,
      DataList: [],
      TunnelDialog: false,
      headers: { 'Authorization': getToken() },
      th: '',
      permission: {
        add: ['admin', 'tunnelInformation:add'],
        edit: ['admin', 'tunnelInformation:edit'],
        del: ['admin', 'tunnelInformation:del']
      },
      rules: {
      },
      queryTypeOptions: [
        { key: 'tunnelInforId', display_name: 'ID' },
        { key: 'projectName', display_name: '项目名称' },
        { key: 'sectionName', display_name: '标段名称' },
        { key: 'tunnelId', display_name: '隧道编号' },
        { key: 'tunnelName', display_name: '隧道名称' },
        { key: 'worksiteName', display_name: '工点名称' },
        { key: 'repairCompany', display_name: '建设单位' },
        { key: 'supervisionCompany', display_name: '监理单位' },
        { key: 'detectionCompany', display_name: '检测单位' },
        { key: 'constructionCompany', display_name: '施工单位' },
        { key: 'userId', display_name: '用户ID' },
        { key: 'userName', display_name: '用户名' },
        { key: 'deptId', display_name: '用户权限' },
        { key: 'time', display_name: '数据新增时间' }
      ]
    }
  },
  computed: {
    ...mapGetters([
      'baseApi',
      'fileUploadApi'
    ])
  },
  methods: {
    // 钩子：在获取表格数据之前执行，false 则代表不获取数据
    [CRUD.HOOK.beforeRefresh]() {
      return true
    },
    // 上传文件
    look(data) {
      select(data).then(response => {
        this.DataList = response
      })
      this.TunnelDialog = true
    },
    cancelCU() {
      this.TunnelDialog = false
    },
    submitUpload() {
      this.$refs.upload.submit()
    },
    handleRemove(file, fileList) {
      console.log(file, fileList)
    },
    handlePreview(file) {
      console.log(file)
    },
    handleAvatarSuccess(file) {
      console.log(file)
    },
    // 上传文件
    upload() {
      this.$refs.upload.submit()
    },
    beforeUpload(file) {
      let isLt2M = true
      isLt2M = file.size / 1024 / 1024 < 100
      if (!isLt2M) {
        this.loading = false
        this.$message.error('上传文件大小不能超过 100MB!')
      }
      this.form.name = file.name
      console.log(file.name)
      return isLt2M
    },
    beforesubmit(response, file, fileList) {
      this.$refs.upload.clearFiles()
    },
    handleSuccess(response, file, fileList) {
      this.crud.notify('上传成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
      this.changeVersion(response)
      this.$refs.upload.clearFiles()
    },
    // 监听上传失败
    handleError(e, file, fileList) {
      const msg = JSON.parse(e.message)
      this.$notify({
        title: msg.message,
        type: 'error',
        duration: 2500
      })
    },
    changeVersion(newVersion) {
      console.log('newVersion', newVersion)
      this.form.beizhu3 = newVersion
    },
    // 改变状态
    updateStatus(data, status) {
      if (status === '未发布') {
        this.$confirm('是否发布隧道信息？', '是否继续？', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          changeStatue(data).then(res => {
            this.crud.toQuery()
            this.crud.notify('发布成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
          })
        })
      } else {
        this.$confirm('是否取消发布隧道信息？', '是否继续？', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          changeStatue(data).then(res => {
            this.crud.toQuery()
            this.crud.notify('已取消发布', CRUD.NOTIFICATION_TYPE.SUCCESS)
          })
        })
      }
    }
  }
}
</script>

<style scoped>
::v-deep .el-image__error, .el-image__placeholder{
  background: none;
}
::v-deep .el-image-viewer__wrapper{
  top: 55px;
}
</style>

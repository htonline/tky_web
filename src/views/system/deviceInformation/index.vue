<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <label class="el-form-item-label">设备类型</label>
        <el-input v-model="query.deviceType" clearable placeholder="设备类型" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <!--
        <label class="el-form-item-label">ID</label>
        <el-input v-model="query.deviceId" clearable placeholder="ID" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">设备型号</label>
        <el-input v-model="query.deviceModel" clearable placeholder="设备型号" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">设备编号</label>
        <el-input v-model="query.deviceBianhao" clearable placeholder="设备编号" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">设备照片</label>
        <el-input v-model="query.devicePhotos" clearable placeholder="设备照片" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">设备证书</label>
        <el-input v-model="query.deviceCertificate" clearable placeholder="设备证书" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        -->
        <rrOperation :crud="crud" />
      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <!--
          <el-form-item label="ID">
            <el-input v-model="form.deviceId" style="width: 370px;" />
          </el-form-item>
          -->
          <el-form-item  label="设备类型" >
            <el-select v-model="form.deviceType" clearable placeholder="请选择" style="width: 150px;" >
              <el-option
                v-for="item in options1"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="设备型号">
            <el-input v-model="form.deviceModel" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="设备编号">
            <el-input v-model="form.deviceBianhao" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="设备照片" >
            <el-button style="margin-left: 10px;" size="small" type="primary" @click="submit">上传照片</el-button>
            <el-input  ref="inp"  v-model="form.devicePhotos" style="width: 120px;" @input="changeVersion" type="hidden"></el-input>
          </el-form-item>
          <el-form-item label="设备证书" >
            <el-button style="margin-left: 10px;" size="small" type="success" @click="submit1">上传证书</el-button>
            <el-input  ref="inpu"  v-model="form.deviceCertificate" style="width: 120px;" @input="changeVersion" type="hidden"></el-input>
          </el-form-item>

          <!--
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
          <el-button type="text" @click="crud.cancelCU">取消</el-button>
          <el-button :loading="crud.status.cu === 2" type="primary" @click="crud.submitCU">确认</el-button>
        </div>
      </el-dialog>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="crud.data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column type="selection" width="55" />
        <el-table-column prop="deviceId" label="ID" />
        <el-table-column prop="deviceType" label="设备类型" />
        <el-table-column prop="deviceModel" label="设备型号" />
        <el-table-column prop="deviceBianhao" label="设备编号" />
        <el-table-column  label="设备照片" width="150px" align="center">
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
        <el-table-column  label="设备证书" width="150px" align="center">
          <template slot-scope="scopes">
            <el-button
              class="filter-item"
              size="mini"
              type="info"
              icon="el-icon-search"
              style="color: #f3ecec"
              @click="look1(scopes.row)"
            >查看</el-button>
          </template>
        </el-table-column>
        <!--
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
        <el-table-column v-if="checkPer(['admin','deviceInformation:edit','deviceInformation:del'])" label="操作" width="150px" align="center">
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
      <el-dialog title="附件材料" :visible.sync="TunnelDialog">
        <el-upload
          multiple
          class="upload-demo"
          ref="upload"
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
          <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传文件</el-button>
          <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-dialog>
      <el-dialog title="附件材料" :visible.sync="TunnelDialog1">
        <el-upload
          multiple
          class="upload-demo"
          ref="upload"
          :action="fileUploadApi + '?name=' + form.name"
          :on-preview="handlePreview"
          :on-remove="handleRemove"
          :auto-upload="false"
          :file-list="fileList"
          :limit="1"
          :before-upload="beforeUpload"
          :headers="headers"
          :on-success="handleSuccess1"
          :on-error="handleError"
        >
          <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
          <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传文件</el-button>
          <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-dialog>
      <el-dialog title="附件材料" :visible.sync="TunnelDialog3">
        <el-table ref="table" v-loading="crud.loading" :data=DataList style="width: 100%;" @selection-change="crud.selectionChangeHandler">
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
                  {{ scope.row.realName}}
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
    </div>
  </div>
</template>

<script>
import crudDeviceInformation from '@/api/system/deviceInformation'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'
import { mapGetters } from 'vuex'
import { getToken } from '@/utils/auth'
import { selectPhotos, selectdeviceCertificate } from '@/api/system/deviceInformation'

const defaultForm = { deviceId: null, deviceType: null, deviceModel: null, deviceBianhao: null, devicePhotos: null, deviceCertificate: null, beizhu1: null, beizhu2: null, beizhu3: null, beizhu4: null, beizhu5: null, beizhu6: null, beizhu7: null, beizhu8: null, beizhu9: null, beizhu10: null, beizhu11: null, beizhu12: null, beizhu13: null, beizhu14: null, beizhu15: null }
export default {
  name: 'DeviceInformation',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: '设备信息', url: 'api/deviceInformation', idField: 'deviceId', sort: 'deviceId,desc', crudMethod: { ...crudDeviceInformation }})
  },
  data() {
    return {
      TunnelDialog3: false,
      TunnelDialog: false,
      TunnelDialog1: false,
      DataList: [],
      DataList2: [],
      headers: { 'Authorization': getToken() },
      options1: [{
        value: '天线',
        label: '天线'
      }, {
        value: '主机',
        label: '主机'
      },
      {
        value: '其他',
        label: '其他'
      }],
      permission: {
        add: ['admin', 'deviceInformation:add'],
        edit: ['admin', 'deviceInformation:edit'],
        del: ['admin', 'deviceInformation:del']
      },
      rules: {
      },
      queryTypeOptions: [
        { key: 'deviceId', display_name: 'ID' },
        { key: 'deviceType', display_name: '设备类型' },
        { key: 'deviceModel', display_name: '设备型号' },
        { key: 'deviceBianhao', display_name: '设备编号' },
        { key: 'devicePhotos', display_name: '设备照片' },
        { key: 'deviceCertificate', display_name: '设备证书' }
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
      selectPhotos(data).then(response => {
        this.DataList = response
        console.log("this.DataList", this.DataList)
      })
      this.TunnelDialog3 = true
    },
    // 上传文件
    look1(data) {
      selectdeviceCertificate(data).then(response => {
        this.DataList = response
      })
      this.TunnelDialog3 = true
    },
    submit() {
      this.TunnelDialog = true
    },
    submit1() {
      this.TunnelDialog1 = true
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
      this.changeVersion(response, 0)
      this.$refs.upload.clearFiles()
    },
    handleSuccess1(response, file, fileList) {
      this.crud.notify('上传成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
      this.changeVersion(response, 1)
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
    changeVersion(newVersion, id) {
      console.log('newVersion', newVersion)
      if (id === 0) {
        this.form.devicePhotos = newVersion
        this.TunnelDialog = false
      }
      if (id === 1) {
        this.form.deviceCertificate = newVersion
        this.TunnelDialog1 = false
      }
    }
  }
}
</script>

<style scoped>

</style>

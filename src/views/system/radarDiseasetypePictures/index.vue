<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <label class="el-form-item-label">ID</label>
        <el-input v-model="query.id" clearable placeholder="ID" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">病害类型</label>
        <el-input v-model="query.diseaseType" clearable placeholder="病害类型" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <rrOperation :crud="crud" />
      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
<!--      编辑-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="ID" prop="id">
            <el-input v-model="form.id" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="病害类型">
            <el-input v-model="form.diseaseType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="设备照片" >
            <el-button style="margin-left: 10px;" size="small" type="primary" @click="submit">上传照片</el-button>
            <el-input  ref="inp"  v-model="form.devicePhotos" style="width: 120px;" @input="changeVersion" type="hidden"></el-input>
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
        <el-table-column prop="id" label="ID" />
        <el-table-column prop="diseaseType" label="病害类型" />
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
        <el-table-column v-if="checkPer(['admin','radarDiseasetypePictures:edit','radarDiseasetypePictures:del'])" label="操作" width="150px" align="center">
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
<!--上传文件Dialog-->
      <el-dialog title="附件材料" :visible.sync="uploadFileDialog">
        <el-upload
          multiple
          class="upload-demo"
          ref="upload"
          :action="pictureUploadApi + '?id=' + form.id"
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
<!--      设备照片Dialog组件-->
      <el-dialog title="雷达图片" :visible.sync="radarPictureDialog">
        <el-table ref="table" v-loading="crud.loading" :data=picturesList style="width: 100%;" @selection-change="crud.selectionChangeHandler">
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
                  :href="baseApi + '/file/图片' + '/' + scope.row.fileName"
                  class="el-link--primary"
                  style="word-break:keep-all;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;color: #1890ff;font-size: 13px;"
                  target="_blank"
                >
                  {{ scope.row.fileName}}
                </a>
              </el-popover>
            </template>
          </el-table-column>
          <el-table-column prop="path" label="预览图">
            <template slot-scope="{row}">
              <el-image
                :src="baseApi + '/file/图片' + '/' + row.fileName"
                :preview-src-list="[baseApi + '/file/图片' + '/' + row.fileName]"
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
<!--          <el-table-column prop="type" label="类别" />-->
          <el-table-column prop="createTime" label="上传日期" />

        </el-table>
      </el-dialog>
    </div>
  </div>
</template>

<script>
import crudRadarDiseasetypePictures from '@/api/radarDiseasetypePictures'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'
import { selectPhotos } from '@/api/system/radarDiseasetypePictures'
import { mapGetters } from 'vuex'
import { getToken } from '@/utils/auth'

const defaultForm = { id: null, diseaseType: null }
export default {
  name: 'RadarDiseasetypePictures',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: 'radarDiseasetypePictures', url: 'api/radarDiseasetypePictures', idField: 'id', sort: 'id,desc', crudMethod: { ...crudRadarDiseasetypePictures }})
  },
  data() {
    return {
      radarPictureDialog: false,
      uploadFileDialog: false,
      picturesList: [],
      headers: {
        'Authorization': getToken()
        // 'Content-Type': 'multipart/form-data'
      },
      permission: {
        add: ['admin', 'radarDiseasetypePictures:add'],
        edit: ['admin', 'radarDiseasetypePictures:edit'],
        del: ['admin', 'radarDiseasetypePictures:del']
      },
      rules: {
        id: [
          { required: true, message: 'ID不能为空', trigger: 'blur' }
        ]
      },
      queryTypeOptions: [
        { key: 'id', display_name: 'ID' },
        { key: 'diseaseType', display_name: '病害类型' }
      ]
    }
  },
  computed: {
    ...mapGetters([
      'baseApi',
      'pictureUploadApi'
    ])
  },
  methods: {
    // 钩子：在获取表格数据之前执行，false 则代表不获取数据
    [CRUD.HOOK.beforeRefresh]() {
      return true
    },
    look(data) {
      // data: 当前点击行的数据：id:1; diseaseType:"路基脱空"
      console.log("data", data)
      selectPhotos(data).then(response => {
        console.log("radarPictureList", response)
        this.picturesList = response
      })
      this.radarPictureDialog = true
    },
    submit() {
      // 点击上传文件之后，会出现选取文件的Dialog
      this.uploadFileDialog = true
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
        this.uploadFileDialog = false
      }
    }
  }
}
</script>

<style scoped>

</style>

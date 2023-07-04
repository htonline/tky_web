<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <label class="el-form-item-label">ID</label>
        <el-input v-model="query.id" clearable placeholder="ID" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">Category1</label>
        <el-input v-model="query.category1" clearable placeholder="Category1" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">Category2</label>
        <el-input v-model="query.category2" clearable placeholder="Category2" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">Category3</label>
        <el-input v-model="query.category3" clearable placeholder="Category3" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">Category4</label>
        <el-input v-model="query.category4" clearable placeholder="Category4" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">Category5</label>
        <el-input v-model="query.category5" clearable placeholder="Category5" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
<!--        <label class="el-form-item-label">Category6</label>-->
<!--        <el-input v-model="query.category6" clearable placeholder="Category6" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category7</label>-->
<!--        <el-input v-model="query.category7" clearable placeholder="Category7" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category8</label>-->
<!--        <el-input v-model="query.category8" clearable placeholder="Category8" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category9</label>-->
<!--        <el-input v-model="query.category9" clearable placeholder="Category9" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category10</label>-->
<!--        <el-input v-model="query.category10" clearable placeholder="Category10" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category11</label>-->
<!--        <el-input v-model="query.category11" clearable placeholder="Category11" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category12</label>-->
<!--        <el-input v-model="query.category12" clearable placeholder="Category12" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category13</label>-->
<!--        <el-input v-model="query.category13" clearable placeholder="Category13" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category14</label>-->
<!--        <el-input v-model="query.category14" clearable placeholder="Category14" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
<!--        <label class="el-form-item-label">Category15</label>-->
<!--        <el-input v-model="query.category15" clearable placeholder="Category15" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />-->
        <rrOperation :crud="crud" />
      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="ID" prop="id">
            <el-input v-model="form.id" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category1">
            <el-input v-model="form.category1" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category2">
            <el-input v-model="form.category2" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category3">
            <el-input v-model="form.category3" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category4">
            <el-input v-model="form.category4" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category5">
            <el-input v-model="form.category5" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category6">
            <el-input v-model="form.category6" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category7">
            <el-input v-model="form.category7" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category8">
            <el-input v-model="form.category8" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category9">
            <el-input v-model="form.category9" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category10">
            <el-input v-model="form.category10" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category11">
            <el-input v-model="form.category11" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category12">
            <el-input v-model="form.category12" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category13">
            <el-input v-model="form.category13" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category14">
            <el-input v-model="form.category14" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="Category15">
            <el-input v-model="form.category15" style="width: 370px;" />
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
        <el-table-column prop="category1" label="Category1" />
        <el-table-column prop="category2" label="Category2" />
        <el-table-column prop="category3" label="Category3" />
        <el-table-column prop="category4" label="Category4" />
        <el-table-column prop="category5" label="Category5" />
        <el-table-column prop="category6" label="Category6" />
        <el-table-column prop="category7" label="Category7" />
        <el-table-column prop="category8" label="Category8" />
        <el-table-column prop="category9" label="Category9" />
        <el-table-column prop="category10" label="Category10" />
        <el-table-column prop="category11" label="Category11" />
        <el-table-column prop="category12" label="Category12" />
        <el-table-column prop="category13" label="Category13" />
        <el-table-column prop="category14" label="Category14" />
        <el-table-column prop="category15" label="Category15" />
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
          :action="pictureUploadApi+'?id='+form.id+'&&category1='+form.category1+'&&category2='+form.category2+'&&category3='+form.category3+'&&category4='+form.category4+'&&category5='+form.category5+'&&category6='+form.category6+'&&category7='+form.category7+'&&category8='+form.category8+'&&category9='+form.category9+'&&category10='+form.category10+'&&category11='+form.category11+'&&category12='+form.category12+'&&category13='+form.category13+'&&category14='+form.category14+'&&category15='+form.category15"
          :on-preview="handlePreview"
          :on-remove="handleRemove"
          :auto-upload="false"
          :file-list="fileList"
          :limit="500"
          :show-file-list="true"
          :before-upload="beforeUpload"
          :headers="headers"
          :on-success="handleSuccess"
          :on-error="handleError"
        >
          <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
          <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传文件</el-button>
          <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb(一次最多上传500张)</div>
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
                  :href="baseApi + '/file/图片/' + scope.row.path + scope.row.fileName"
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
                :src="baseApi + '/file/图片/' + row.path + row.fileName"
                :preview-src-list="[baseApi + '/file/图片/' + row.path + row.fileName]"
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

const defaultForm = { id: null, category1: null, category2: null, category3: null, category4: null, category5: null, category6: null, category7: null, category8: null, category9: null, category10: null, category11: null, category12: null, category13: null, category14: null, category15: null }
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
      picturePath: '',
      headers: {
        'Authorization': getToken()
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
        { key: 'category1', display_name: 'Category1' },
        { key: 'category2', display_name: 'Category2' },
        { key: 'category3', display_name: 'Category3' },
        { key: 'category4', display_name: 'Category4' },
        { key: 'category5', display_name: 'Category5' },
        { key: 'category6', display_name: 'Category6' },
        { key: 'category7', display_name: 'Category7' },
        { key: 'category8', display_name: 'Category8' },
        { key: 'category9', display_name: 'Category9' },
        { key: 'category10', display_name: 'Category10' },
        { key: 'category11', display_name: 'Category11' },
        { key: 'category12', display_name: 'Category12' },
        { key: 'category13', display_name: 'Category13' },
        { key: 'category14', display_name: 'Category14' },
        { key: 'category15', display_name: 'Category15' }
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
    // 从字符串路径中,提取它的数字文件名，转化为数字
    extractNumber(str) {
      const numberPart = str.match(/\d+/)[0]
      return parseInt(numberPart, 10)
    },
    // 自定义排序函数
    customSort(a, b) {
      // 提取需要比较的部分，如 "1.png" 的数字部分
      const numberA = this.extractNumber(a)
      const numberB = this.extractNumber(b)
      // 比较数字部分
      return numberA - numberB
    },
    look(data) {
      // data: 当前点击行的数据：id:1; diseaseType:"路基脱空"
      console.log("data", data)
      selectPhotos(data).then(response => {
        console.log("radarPictureList1", response)
        this.picturesList = response
        // 路径清空
        this.picturePath = ''
        for (const [key, value] of Object.entries(data)) {
          if (key !== 'id') {
            this.picturePath += value + '/'
          }
        }
        for (let i = 0; i < this.picturesList.length; i++) {
          // 将每个元素的 path 属性设置为 this.path
          this.picturesList[i].path = this.picturePath
        }

        console.log("picturePath", this.picturePath)
        console.log("picturesList21321", this.picturesList)

        this.picturesList.sort((a, b) => this.customSort(a.fileName, b.fileName))

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

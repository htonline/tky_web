<template>
  <!--  隧道衬砌信息管理 - 报检管理 -->
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div v-if="crud.props.searchToggle">
        <!-- 搜索 -->
        <!--
        <label class="el-form-item-label">ID</label>
        <el-input v-model="query.testInforId" clearable placeholder="ID" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        -->
        <label class="el-form-item-label">报检号</label>
        <el-input v-model="query.testId" clearable placeholder="报检号" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <label class="el-form-item-label">申请检测时间</label>
        <el-input v-model="query.testTime" clearable placeholder="申请检测时间" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
        <!--
         <label class="el-form-item-label">待检区段起始里程</label>
         <el-input v-model="query.testStartingDistance" clearable placeholder="待检区段起始里程" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">待检区段结束里程</label>
         <el-input v-model="query.testEndingDistance" clearable placeholder="待检区段结束里程" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">待检区段长度</label>
         <el-input v-model="query.testLength" clearable placeholder="待检区段长度" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">围岩类型</label>
         <el-input v-model="query.wallRockType" clearable placeholder="围岩类型" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">初支厚度</label>
         <el-input v-model="query.supportTickness" clearable placeholder="初支厚度" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">间距(m/榀)</label>
         <el-input v-model="query.separationDistance" clearable placeholder="间距(m/榀)" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">钢筋网间距</label>
         <el-input v-model="query.meshDistance" clearable placeholder="钢筋网间距" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">环向钢筋间距</label>
         <el-input v-model="query.annularBarDistance" clearable placeholder="环向钢筋间距" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">钢筋保护厚度</label>
         <el-input v-model="query.reinforPrtTickness" clearable placeholder="钢筋保护厚度" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">二次衬砌厚度-拱部</label>
         <el-input v-model="query.secLineArchTickness" clearable placeholder="二次衬砌厚度-拱部" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">二次衬砌厚度-边墙</label>
         <el-input v-model="query.secLineWallTickness" clearable placeholder="二次衬砌厚度-边墙" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">二次衬砌厚度-仰拱</label>
         <el-input v-model="query.secLineInverArchTickness" clearable placeholder="二次衬砌厚度-仰拱" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">二次衬砌厚度-填充</label>
         <el-input v-model="query.secLineFilerTickness" clearable placeholder="二次衬砌厚度-填充" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">项目名称</label>
         <el-input v-model="query.projectName" clearable placeholder="项目名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">标段名称</label>
         <el-input v-model="query.sectionName" clearable placeholder="标段名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">隧道名称</label>
         <el-input v-model="query.tunnelName" clearable placeholder="隧道名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">工点名称</label>
         <el-input v-model="query.worksiteName" clearable placeholder="工点名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         <label class="el-form-item-label">状态</label>
         <el-input v-model="query.statute" clearable placeholder="状态" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
         -->
        <rrOperation :crud="crud" />
      </div>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission">
        <!--表单组件-->
        <!-- 新增 -->
        <el-button
          slot="left"
          v-permission="['admin','testInformation:look']"
          class="filter-item"
          size="mini"
          type="primary"
          icon="el-icon-plus"
          @click="lookTunnelMess()"
        >新增
        </el-button>
        <div class="user-right" />
      </crudOperation>
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="1000px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-row>
            <div>
              <el-divider>隧道基本信息</el-divider>
            </div>
          </el-row>
          <el-row>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">项目名称</div>
                <el-input v-model="form.projectName" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">标段名称</div>
                <el-input v-model="form.sectionName" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">隧道名称</div>
                <el-input v-model="form.tunnelName" style="width: 250px;" />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">工点名称</div>
                <el-input v-model="form.worksiteName" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">待检区段起始里程</div>
                <el-input v-model="form.beizhu2" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">待检区段结束里程</div>
                <el-input v-model="form.beizhu3" style="width: 250px;" />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="8">
              <el-form-item>
                <div class="sub-title">待检区段长度</div>
                <el-input v-model="form.beizhu4" style="width: 250px;" />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <div>
              <el-divider>初始化基本信息</el-divider>
            </div>
          </el-row>
          <el-row>
            <el-col :span="7">
              <el-form-item>
                <div class="sub-title">围岩类型</div>
                <el-input v-model="form.wallRockType" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">初支厚度(cm)</div>
                <el-input v-model="form.supportTickness" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">间距(m/榀)</div>
                <el-input v-model="form.separationDistance" style="width: 250px;" />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">钢筋网间距(cm)</div>
                <el-input v-model="form.meshDistance" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">环向钢筋间距(cm)</div>
                <el-input v-model="form.annularBarDistance" style="width: 250px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">钢筋保护厚度(mm)</div>
                <el-input v-model="form.reinforPrtTickness" style="width: 150px;" />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row title="二次衬砌厚度">
            <el-col :span="6">
              <el-form-item label="">
                <div class="sub-title">二次衬砌厚度(cm):拱部</div>
                <el-input v-model="form.secLineArchTickness" style="width: 150px;" />
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="">
                <div class="sub-title">二次衬砌厚度(cm):边墙</div>
                <el-input v-model="form.secLineWallTickness" style="width: 150px;" />
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="">
                <div class="sub-title">二次衬砌厚度(cm):仰拱</div>
                <el-input v-model="form.secLineInverArchTickness" style="width: 150px;" />
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="">
                <div class="sub-title">二次衬砌厚度(cm):填充</div>
                <el-input v-model="form.secLineFilerTickness" style="width: 150px;" />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <div>
              <el-divider>衬砌报检基本信息</el-divider>
            </div>
          </el-row>
          <el-row>
            <el-col :span="5">
              <el-form-item>
                <div class="sub-title">施工单位</div>
                <el-input v-model="form.beizhu5" style="width: 180px;">{{ user.nickName }}</el-input>
              </el-form-item>
            </el-col>
            <el-col :span="5">
              <el-form-item>
                <div class="sub-title">联系人</div>
                <el-input v-model="form.beizhu6" style="width: 180px;">{{ user.username }}</el-input>
              </el-form-item>
            </el-col>
            <el-col :span="5">
              <el-form-item>
                <div class="sub-title">联系方式</div>
                <el-input v-model="form.beizhu7" style="width: 180px;" />
              </el-form-item>
            </el-col>
            <el-col :span="5">
              <el-form-item>
                <div class="sub-title">检测单位</div>
                <!-- <el-input v-model="defaultForms.beizhu8" style="width: 170px;" />   -->
                <el-select
                  v-model="form.beizhu8"
                  placeholder="选择检测单位"
                  clearable
                  style="width: 170px;"
                  @focus="handleQuery"
                >
                  <el-option
                    v-for="item in dishesInfoList"
                    :key="item.nickName"
                    :value="item.nickName"
                    :label="item.nickName"
                  />
                </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="5">
              <el-form-item>
                <div class="sub-title">监理单位</div>
                <!-- <el-input v-model="defaultForms.beizhu9" style="width: 180px;" /> -->
                <el-select
                  v-model="form.beizhu9"
                  placeholder="选择监理单位"
                  clearable
                  style="width: 170px;"
                  @focus="handleQuery1"
                >
                  <el-option
                    v-for="item in dishesInfoList1"
                    :key="item.nickName"
                    :value="item.nickName"
                    :label="item.nickName"
                  />
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :span="4">
              <el-form-item>
                <div class="sub-title">检测方式</div>
                <el-select v-model="form.beizhu10" clearable placeholder="请选择" style="width: 150px;">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :span="4">
              <el-form-item>
                <div class="sub-title">检测方法</div>
                <el-select v-model="form.beizhu11" clearable placeholder="请选择" style="width: 150px;">
                  <el-option
                    v-for="item in options1"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">申请检测时间</div>
                <el-date-picker
                  v-model="form.testTime"
                  type="datetime"
                  placeholder="选择日期时间"
                />
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>

            <el-col :span="5">
              <el-form-item label="">
                <div class="sub-title">检测部位</div>
                <el-input v-model="form.beizhu12" style="width: 150px;" />
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="">
                <div class="sub-title">隧道浇筑时间</div>
                <el-date-picker
                  v-model="form.beizhu13"
                  type="datetime"
                  placeholder="选择日期时间"
                />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">起始里程</div>
                <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="form.beizhu16" style="width: 60px;" /><span> + </span><el-input v-model="form.beizhu14" style="width: 60px;" />
              </el-form-item>
            </el-col>
            <el-col :span="7">
              <el-form-item label="">
                <div class="sub-title">结束里程</div>
                <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="form.beizhu17" style="width: 60px;" /><span> + </span><el-input v-model="form.beizhu15" style="width: 60px;" />
              </el-form-item>
            </el-col>
            <el-col :span="5">
              <el-form-item label="">
                <div class="sub-title">检测长度</div>
                <el-input v-model="form.testLength" style="width: 100px;" />
              </el-form-item>
            </el-col>
          </el-row>

        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="text" @click="crud.cancelCU">取消</el-button>
          <el-button :loading="crud.status.cu === 2" type="primary" @click="crud.submitCU">确认</el-button>
        </div>
      </el-dialog>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="crud.data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column type="selection" width="55" />
        <!--
        <el-table-column prop="testInforId" label="ID" />

        <el-table-column prop="" label="状态" />
        -->
        <el-table-column prop="beizhu26" label="检测报告">
          <template slot-scope="scope">
            <el-button mutilline="true" type="text" @click="updateDetectionSummaryDialog(scope.row)">上传</el-button>
            <el-button mutilline="true" type="text" @click="downloadDetectionSummary(scope.row,scope.row.beizhu26)">下载</el-button>
            {{ scope.row.beizhu26 }}
            <el-dialog append-to-body :close-on-click-modal="false" :visible.sync="uploadDetectionSummaryDialogIs" :title="crud.status.add ? '文件上传' : '编辑文件'" width="500px">
              <el-form ref="form" :model="form" size="small" label-width="80px">
                <el-form-item label="上传">
                  <!--   上传文件   -->
                  <el-upload
                    ref="upload"
                    :limit="1"
                    :before-upload="beforeUpload"
                    :auto-upload="false"
                    :headers="headers"
                    :on-success="handleSuccess"
                    :on-error="handleError"
                    :action="updateDetectionSummaryPath"
                    :data="{data:dataid}"
                  >
                    <div class="eladmin-upload" onclick=""><i class="el-icon-upload" /> 添加文件</div>
                    <div slot="tip" class="el-upload__tip">可上传任意格式文件，且不超过100M</div>
                  </el-upload>
                </el-form-item>
              </el-form>
              <div slot="footer" class="dialog-footer">
                <el-button type="text" @click="cancel()">取消</el-button>
                <el-button type="primary" @click="upload">确认</el-button>
              </div>
            </el-dialog>
          </template>
        </el-table-column>
        <el-table-column prop="projectName" label="项目名称" />
        <el-table-column prop="sectionName" label="标段名称" />
        <el-table-column prop="tunnelName" label="隧道名称" />
        <el-table-column prop="worksiteName" label="工点名称" />
        <el-table-column prop="testId" label="报检号" />
        <el-table-column prop="testTime" label="申请检测时间" />
        <el-table-column prop="testStartingDistance" label="待检区段起始里程" />
        <el-table-column prop="testEndingDistance" label="待检区段结束里程" />
        <el-table-column prop="testLength" label="待检区段长度" />
        <el-table-column prop="wallRockType" label="围岩类型" />
        <el-table-column prop="supportTickness" label="初支厚度" />
        <el-table-column prop="separationDistance" label="间距(m/榀)" />
        <el-table-column prop="meshDistance" label="钢筋网间距" />
        <el-table-column prop="annularBarDistance" label="环向钢筋间距" />
        <el-table-column prop="reinforPrtTickness" label="钢筋保护厚度" />
        <el-table-column prop="reinforPrtTickness" label="二次衬砌厚度" align="center">
          <el-table-column prop="secLineArchTickness" label="拱部" />
          <el-table-column prop="secLineWallTickness" label="边墙" />
          <el-table-column prop="secLineInverArchTickness" label="仰拱" />
          <el-table-column prop="secLineFilerTickness" label="填充" />
        </el-table-column>
        <el-table-column prop="statute" label="报检单状态" />
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
        <el-table-column label="审核" width="150px" align="center">
          <template slot-scope="scope">
            <el-button
              slot="right"
              v-permission="['admin','testInformation:JianceCheck']"
              class="filter-item"
              size="mini"
              type="warning"
              icon="el-icon-check"
              @click="JianceCheck(scope.row)"
            >检测单位审核</el-button>
            <el-button
              slot="right"
              v-permission="['admin','testInformation:JiliCheck']"
              class="filter-item"
              size="mini"
              type="warning"
              icon="el-icon-check"
              @click="JianliCheck(scope.row)"
            >监理单位审核</el-button>
            <el-button
              slot="right"
              v-permission="['admin','testInformation:SigongCheck']"
              class="filter-item"
              size="mini"
              type="warning"
              icon="el-icon-check"
              @click="SigongCheck(scope.row)"
            >施工单位查看</el-button>
          </template>
        </el-table-column>
        <el-table-column v-if="checkPer(['testInformation:edit','testInformation:del','testInformation:createErweima'])" label="操作" width="150px" align="center">
          <template slot-scope="scope">
            <el-button
              slot="right"
              v-permission="['admin','testInformation:createErweima']"
              class="filter-item"
              size="mini"
              type="info"
              icon="el-icon-tickets"
              @click="createErweima(scope.row)"
            >二维码</el-button>
            <udOperation
              :data="scope.row"
              :permission="permission"
            />
          </template>
        </el-table-column>
      </el-table>
      <el-dialog :visible.sync="errordialog" title="二维码" append-to-body top="30px" width="30%">
        <img :src="errorInfo" style="width:500px;height:600px">
      </el-dialog>
      <el-dialog title="隧道信息" :visible.sync="TunnelDialog" width="60%">
        <div v-if="crud.props.searchToggle">
          <label class="el-form-item-label">项目名称</label>
          <el-input v-model="query.projectName" clearable placeholder="项目名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
          <label class="el-form-item-label">标段名称</label>
          <el-input v-model="query.tunnelId" clearable placeholder="隧道编号" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
          <label class="el-form-item-label">隧道名称</label>
          <el-input v-model="query.tunnelName" clearable placeholder="隧道名称" style="width: 185px;" class="filter-item" @keyup.enter.native="crud.toQuery" />
          <rrOperation :crud="crud" />
        </div>
        <el-table ref="table" v-loading="crud.loading" :data="DataList" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
          <el-table-column prop="tunnelInforId" label="序号" />
          <el-table-column prop="projectName" label="项目名称" />
          <el-table-column prop="sectionName" label="标段名称" />
          <el-table-column prop="tunnelId" label="隧道编号" />
          <el-table-column prop="tunnelName" label="隧道名称" />
          <el-table-column prop="worksiteName" label="工点名称" />
          <el-table-column prop="tunnelStartingDistance" label="隧道起始里程" />
          <el-table-column prop="tunnelEndingDistance" label="隧道结束里程" />
          <el-table-column prop="tunnelLength" label="隧道长度" />
          <el-table-column label="状态" width="170px" align="center" prop="beizhu4" />
          <el-table-column label="附件材料" width="150px" align="center">
            <template slot-scope="scopes">
              <el-button
                class="filter-item"
                size="mini"
                type="info"
                icon="baojiandan"
                style="color: #f3ecec"
                @click="look()"
              >申请报检</el-button>
            </template>
          </el-table-column>
        </el-table>
        <!--分页组件-->
        <pagination />
      </el-dialog>

      <!--分页组件-->
      <pagination />
    </div>
    <el-dialog :visible.sync="openTuneldialog" :close-on-click-modal="false" title="隧道信息" append-to-body width="1300px" @closed="cancelOpenTuneldialog">
      <div class="head-container">
        <div>
          <label class="el-form-item-label">隧道名称</label>
          <el-input ref="tunnelName" v-model="query.tunnelName" clearable placeholder="隧道名称" style="width: 185px;" class="filter-item" />
          <el-button class="filter-item" size="mini" type="success" icon="el-icon-search" @click="serach()">搜索</el-button>
        </div>
        <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      </div>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="Data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column prop="projectName" label="项目名称" />
        <el-table-column prop="sectionName" label="标段名称" />
        <el-table-column prop="tunnelId" label="隧道编号" />
        <el-table-column prop="tunnelName" label="隧道名称" />
        <el-table-column prop="worksiteName" label="工点名称" />
        <el-table-column prop="tunnelStartingDistance" label="隧道起始里程" />
        <el-table-column prop="tunnelEndingDistance" label="隧道结束里程" />
        <el-table-column prop="tunnelLength" label="隧道长度" />
        <el-table-column label="附件材料" width="150px" align="center">
          <template slot-scope="scope">
            <el-button
              class="filter-item"
              size="mini"
              type="info"
              icon="el-icon-search"
              style="color: #f3ecec"
              @click="look(scope.row)"
            >查看</el-button>
          </template>
        </el-table-column>
        <el-table-column label="状态" width="170px" align="center" prop="beizhu4" />
        <el-table-column label="操作" width="150px" align="center">
          <template slot-scope="scope">
            <el-button
              v-permission="['admin','testInformation:createTest']"
              class="filter-item"
              size="mini"
              type="warning"
              icon="el-icon-tickets"
              style="color: #aa0fa7"
              @click="createTest(scope.row)"
            >申请报检</el-button>
          </template>
        </el-table-column>
      </el-table>
      <!--分页组件-->
      <pagination />
    </el-dialog>
    <el-dialog title="附件材料" :visible.sync="TunnelInfoDialog">
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
      </el-table>
    </el-dialog>
    <el-dialog :close-on-click-modal="false" :visible.sync="BaojianDialog" title="新增报检单" width="1000px" :show-close="false" @closed="delmmess(defaultForms)">
      <el-form ref="defaultForms" :model="defaultForms" :rules="rules" size="small" label-width="80px">
        <el-row>
          <div>
            <el-divider>隧道基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">项目名称</div>
              <el-input v-model="defaultForms.projectName" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">标段名称</div>
              <el-input v-model="defaultForms.sectionName" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">隧道名称</div>
              <el-input v-model="defaultForms.tunnelName" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">工点名称</div>
              <el-input v-model="defaultForms.worksiteName" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段起始里程</div>
              <el-input v-model="defaultForms.beizhu2" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段结束里程</div>
              <el-input v-model="defaultForms.beizhu3" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="8">
            <el-form-item>
              <div class="sub-title">待检区段长度</div>
              <el-input v-model="defaultForms.beizhu4" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>初始化基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">围岩类型</div>
              <el-input v-model="defaultForms.wallRockType" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">初支厚度(cm)</div>
              <el-input v-model="defaultForms.supportTickness" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">间距(m/榀)</div>
              <el-input v-model="defaultForms.separationDistance" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">钢筋网间距(cm)</div>
              <el-input v-model="defaultForms.meshDistance" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">环向钢筋间距(cm)</div>
              <el-input v-model="defaultForms.annularBarDistance" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">钢筋保护厚度(mm)</div>
              <el-input v-model="defaultForms.reinforPrtTickness" style="width: 150px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row title="二次衬砌厚度">
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):拱部</div>
              <el-input v-model="defaultForms.secLineArchTickness" style="width: 150px;" />
            </el-form-item>
          </el-col>
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):边墙</div>
              <el-input v-model="defaultForms.secLineWallTickness" style="width: 150px;" />
            </el-form-item>
          </el-col>
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):仰拱</div>
              <el-input v-model="defaultForms.secLineInverArchTickness" style="width: 150px;" />
            </el-form-item>
          </el-col>
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):填充</div>
              <el-input v-model="defaultForms.secLineFilerTickness" style="width: 150px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>衬砌报检基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">施工单位</div>
              <el-input v-model="defaultForms.beizhu5" style="width: 180px;">{{ user.nickName }}</el-input>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">联系人</div>
              <el-input v-model="defaultForms.beizhu6" style="width: 180px;">{{ user.username }}</el-input>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">联系方式</div>
              <el-input v-model="defaultForms.beizhu7" style="width: 180px;" />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">检测单位</div>
              <!-- <el-input v-model="defaultForms.beizhu8" style="width: 170px;" />   -->
              <el-select
                v-model="defaultForms.beizhu8"
                placeholder="选择检测单位"
                clearable
                style="width: 170px;"
                @focus="handleQuery()"
              >
                <el-option
                  v-for="item in dishesInfoList"
                  :key="item.nickName"
                  :value="item.nickName"
                  :label="item.nickName"
                />
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">监理单位</div>
              <!-- <el-input v-model="defaultForms.beizhu9" style="width: 180px;" /> -->
              <el-select
                v-model="defaultForms.beizhu9"
                placeholder="选择监理单位"
                clearable
                style="width: 170px;"
                @focus="handleQuery1()"
              >
                <el-option
                  v-for="item in dishesInfoList1"
                  :key="item.nickName"
                  :value="item.nickName"
                  :label="item.nickName"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="4">
            <el-form-item>
              <div class="sub-title">检测方式</div>
              <el-select v-model="defaultForms.beizhu10" clearable placeholder="请选择" style="width: 150px;">
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="4">
            <el-form-item>
              <div class="sub-title">检测方法</div>
              <el-select v-model="defaultForms.beizhu11" clearable placeholder="请选择" style="width: 150px;">
                <el-option
                  v-for="item in options1"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">申请检测时间</div>
              <el-date-picker
                v-model="defaultForms.testTime"
                type="datetime"
                placeholder="选择日期时间"
              />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>

          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">检测部位</div>
              <el-input v-model="defaultForms.beizhu12" style="width: 150px;" />
            </el-form-item>
          </el-col>
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">隧道浇筑时间</div>
              <el-date-picker
                v-model="defaultForms.beizhu13"
                type="datetime"
                placeholder="选择日期时间"
              />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">起始里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu16" style="width: 60px;" /><span> + </span><el-input v-model="defaultForms.beizhu14" style="width: 60px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">结束里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu17" style="width: 60px;" /><span> + </span><el-input v-model="defaultForms.beizhu15" style="width: 60px;" />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">检测长度</div>
              <el-input v-model="defaultForms.testLength" style="width: 120px;" />
            </el-form-item>
          </el-col>
        </el-row>

      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button type="text" @click="cancelCU()">取消</el-button>
        <el-button :loading="crud.status.cu === 2" type="primary" @click="submitForm(defaultForms)">提交报检单</el-button>
      </div>
    </el-dialog>
    <el-dialog :close-on-click-modal="false" :visible.sync="shigongdanweiShenHeDialog" title="查看报检单审核进度" width="1000px">
      <el-form ref="defaultForms" :model="defaultForms" :rules="rules" size="small" label-width="80px">
        <el-row>
          <div>
            <el-divider>隧道基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">项目名称</div>
              <el-input v-model="defaultForms.projectName" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">标段名称</div>
              <el-input v-model="defaultForms.sectionName" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">隧道名称</div>
              <el-input v-model="defaultForms.tunnelName" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">工点名称</div>
              <el-input v-model="defaultForms.worksiteName" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段起始里程</div>
              <el-input v-model="defaultForms.beizhu2" style="width: 250px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段结束里程</div>
              <el-input v-model="defaultForms.beizhu3" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="8">
            <el-form-item>
              <div class="sub-title">待检区段长度</div>
              <el-input v-model="defaultForms.beizhu4" style="width: 250px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>衬砌报检基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">施工单位</div>
              <el-input v-model="defaultForms.beizhu5" style="width: 180px;">{{ user.nickName }}</el-input>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">联系人</div>
              <el-input v-model="defaultForms.beizhu6" style="width: 180px;">{{ user.username }}</el-input>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">联系方式</div>
              <el-input v-model="defaultForms.beizhu7" style="width: 180px;" />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">检测单位</div>
              <!-- <el-input v-model="defaultForms.beizhu8" style="width: 170px;" />   -->
              <el-select
                v-model="defaultForms.beizhu8"
                placeholder="选择检测单位"
                clearable
                style="width: 170px;"
                @focus="handleQuery"
              >
                <el-option
                  v-for="item in dishesInfoList"
                  :key="item.nickName"
                  :value="item.nickName"
                  :label="item.nickName"
                />
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">监理单位</div>
              <!-- <el-input v-model="defaultForms.beizhu9" style="width: 180px;" /> -->
              <el-select
                v-model="defaultForms.beizhu9"
                placeholder="选择监理单位"
                clearable
                style="width: 170px;"
                @focus="handleQuery1"
              >
                <el-option
                  v-for="item in dishesInfoList1"
                  :key="item.nickName"
                  :value="item.nickName"
                  :label="item.nickName"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="4">
            <el-form-item>
              <div class="sub-title">检测方式</div>
              <el-select v-model="defaultForms.beizhu10" clearable placeholder="请选择" style="width: 150px;">
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="4">
            <el-form-item>
              <div class="sub-title">检测方法</div>
              <el-select v-model="defaultForms.beizhu11" clearable placeholder="请选择" style="width: 150px;">
                <el-option
                  v-for="item in options1"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">申请检测时间</div>
              <el-date-picker
                v-model="defaultForms.testTime"
                type="datetime"
                placeholder="选择日期时间"
              />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>

          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">检测部位</div>
              <el-input v-model="defaultForms.beizhu12" style="width: 150px;" />
            </el-form-item>
          </el-col>
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">隧道浇筑时间</div>
              <el-date-picker
                v-model="defaultForms.beizhu13"
                type="datetime"
                placeholder="选择日期时间"
              />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">起始里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu16" style="width: 60px;" /><span> + </span><el-input v-model="defaultForms.beizhu14" style="width: 60px;" />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">结束里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu17" style="width: 60px;" /><span> + </span><el-input v-model="defaultForms.beizhu15" style="width: 60px;" />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">检测长度</div>
              <el-input v-model="defaultForms.testLength" style="width: 120px;" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>确认检测计划</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-container>
            <el-col :span="10">
              <el-form-item>
                <el-aside width="200px" align="center">审核流程</el-aside>
              </el-form-item>
            </el-col>
            <el-col>
              <el-form-item>
                <el-main>
                  <div class="block">
                    <el-timeline>
                      <el-timeline-item
                        v-for="(activity, index) in activities"
                        :key="index"
                        :icon="activity.icon"
                        :type="activity.type"
                        :color="activity.color"
                        :size="activity.size"
                        :timestamp="activity.timestamp"
                      >
                        {{ activity.content }}
                      </el-timeline-item>
                    </el-timeline>
                  </div>
                </el-main>
              </el-form-item>
            </el-col>
          </el-container>
        </el-row>

      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button type="primary" @click="cancelDialog()">取消</el-button>
      </div>
    </el-dialog>
    <el-dialog :close-on-click-modal="false" :visible.sync="jianlidanweishenheDialog" title="监理单位审核报检单" width="1000px">
      <el-form ref="defaultForms" :model="defaultForms" :rules="rules" size="small" label-width="80px">
        <el-row>
          <div>
            <el-divider>隧道基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">项目名称</div>
              <el-input v-model="defaultForms.projectName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">标段名称</div>
              <el-input v-model="defaultForms.sectionName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">隧道名称</div>
              <el-input v-model="defaultForms.tunnelName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">工点名称</div>
              <el-input v-model="defaultForms.worksiteName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段起始里程</div>
              <el-input v-model="defaultForms.beizhu2" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段结束里程</div>
              <el-input v-model="defaultForms.beizhu3" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段长度</div>
              <el-input v-model="defaultForms.beizhu4" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">施工单位</div>
              <el-input v-model="defaultForms.beizhu5" style="width: 180px;" disabled>{{ user.nickName }}</el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>衬砌报检基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">申请检测时间</div>
              <el-date-picker
                v-model="defaultForms.testTime"
                type="datetime"
                placeholder="选择日期时间"
                disabled
              />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">起始里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu16" style="width: 60px;" disabled /><span> + </span><el-input v-model="defaultForms.beizhu14" style="width: 60px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">结束里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu17" style="width: 60px;" disabled /><span> + </span><el-input v-model="defaultForms.beizhu15" style="width: 60px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">检测长度</div>
              <el-input v-model="defaultForms.testLength" style="width: 120px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):拱部</div>
              <el-input v-model="defaultForms.secLineArchTickness" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):边墙</div>
              <el-input v-model="defaultForms.secLineWallTickness" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):仰拱</div>
              <el-input v-model="defaultForms.secLineInverArchTickness" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">二次衬砌厚度(cm):填充</div>
              <el-input v-model="defaultForms.secLineFilerTickness" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">围岩类型</div>
              <el-input v-model="defaultForms.wallRockType" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">初支厚度(cm)</div>
              <el-input v-model="defaultForms.supportTickness" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">间距(m/榀)</div>
              <el-input v-model="defaultForms.separationDistance" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">钢筋网间距(cm)</div>
              <el-input v-model="defaultForms.meshDistance" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">环向钢筋间距(cm)</div>
              <el-input v-model="defaultForms.annularBarDistance" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">钢筋保护厚度(mm)</div>
              <el-input v-model="defaultForms.reinforPrtTickness" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>确认检测计划</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-container>
            <el-col :span="10">
              <el-form-item>
                <el-aside width="200px" align="center">审核流程</el-aside>
              </el-form-item>
            </el-col>
            <el-col>
              <el-form-item>
                <el-main>
                  <div class="block">
                    <el-timeline>
                      <el-timeline-item
                        v-for="(activity, index) in activities"
                        :key="index"
                        :icon="activity.icon"
                        :type="activity.type"
                        :color="activity.color"
                        :size="activity.size"
                        :timestamp="activity.timestamp"
                      >
                        {{ activity.content }}
                      </el-timeline-item>
                    </el-timeline>
                  </div>
                </el-main>
              </el-form-item>
            </el-col>
          </el-container>
        </el-row>
        <el-row>
          <el-container>
            <el-col :span="10">
              <el-form-item>
                <el-aside width="200px" align="center">审核意见</el-aside>
              </el-form-item>
            </el-col>
            <el-col>
              <el-form-item>
                <div>
                  <el-radio v-model="defaultForms.beizhu19" label="1" border>同意</el-radio>
                  <el-radio v-model="defaultForms.beizhu19" label="0" border>不同意</el-radio>
                </div>
              </el-form-item>
            </el-col>
          </el-container>
        </el-row>
        <el-row>
          <el-container>
            <el-col :span="6">
              <el-form-item>
                <el-aside width="200px" align="center">备注信息</el-aside>
              </el-form-item>
            </el-col>
            <el-col :span="15">
              <el-form-item>
                <el-input
                  v-model="defaultForms.beizhu20"
                  type="textarea"
                  :rows="4"
                  placeholder="请输入内容"
                />
              </el-form-item>
            </el-col>
          </el-container>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button type="text" @click=" cancelDialog()">取消</el-button>
        <el-button v-permission="['admin','testInformation:jiliupdateTestInformation']" :loading="crud.status.cu === 2" type="primary" @click="submitDeForm(defaultForms)">提交报检单</el-button>
      </div>
    </el-dialog>
    <el-dialog :close-on-click-modal="false" :visible.sync="TestShenHeDialog" title="检测单位确认报检单信息" width="1000px" style="color: #FFBA00">
      <el-form ref="defaultForms" :model="defaultForms" :rules="rules" size="small" label-width="80px">
        <el-row>
          <div>
            <el-divider>隧道基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">项目名称</div>
              <el-input v-model="defaultForms.projectName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">标段名称</div>
              <el-input v-model="defaultForms.sectionName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">隧道名称</div>
              <el-input v-model="defaultForms.tunnelName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">工点名称</div>
              <el-input v-model="defaultForms.worksiteName" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段起始里程</div>
              <el-input v-model="defaultForms.beizhu2" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item>
              <div class="sub-title">待检区段结束里程</div>
              <el-input v-model="defaultForms.beizhu3" style="width: 250px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">待检区段长度</div>
              <el-input v-model="defaultForms.beizhu4" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">施工单位</div>
              <el-input v-model="defaultForms.beizhu5" style="width: 180px;" disabled>{{ user.nickName }}</el-input>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">联系人</div>
              <el-input v-model="defaultForms.beizhu6" style="width: 180px;" disabled>{{ user.username }}</el-input>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">联系方式</div>
              <el-input v-model="defaultForms.beizhu7" style="width: 180px;" disabled />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">监理单位</div>
              <!-- <el-input v-model="defaultForms.beizhu9" style="width: 180px;" /> -->
              <el-select
                v-model="defaultForms.beizhu9"
                placeholder="选择监理单位"
                clearable
                style="width: 170px;"
                disabled
                @focus="handleQuery1"
              >
                <el-option
                  v-for="item in dishesInfoList1"
                  :key="item.nickName"
                  :value="item.nickName"
                  :label="item.nickName"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">检测方式</div>
              <el-select v-model="defaultForms.beizhu10" clearable placeholder="请选择" style="width: 150px;" disabled>
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">检测方法</div>
              <el-select v-model="defaultForms.beizhu11" clearable placeholder="请选择" style="width: 150px;" disabled>
                <el-option
                  v-for="item in options1"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">申请检测时间</div>
              <el-date-picker
                v-model="defaultForms.testTime"
                type="datetime"
                placeholder="选择日期时间"
                disabled
              />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>衬砌报检基本信息</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-col :span="4">
            <el-form-item label="">
              <div class="sub-title">检测部位</div>
              <el-input v-model="defaultForms.beizhu12" style="width: 150px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="6">
            <el-form-item label="">
              <div class="sub-title">隧道浇筑时间</div>
              <el-date-picker
                v-model="defaultForms.beizhu12"
                style="width: 200px;"
                type="datetime"
                placeholder="选择日期时间"
                disabled
              />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">起始里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu16" style="width: 60px;" disabled /><span> + </span><el-input v-model="defaultForms.beizhu14" style="width: 60px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="7">
            <el-form-item label="">
              <div class="sub-title">结束里程</div>
              <el-input style="width: 60px;" disabled value="DK" /> <el-input v-model="defaultForms.beizhu17" style="width: 60px;" disabled /><span> + </span><el-input v-model="defaultForms.beizhu15" style="width: 60px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item label="">
              <div class="sub-title">检测长度</div>
              <el-input v-model="defaultForms.testLength" style="width: 120px;" disabled />
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">检测设备：天线</div>
              <el-select
                v-model="defaultForms.beizhu24"
                placeholder="选择天线"
                clearable
                style="width: 170px;"
                @focus="handleQueryTianxian"
              >
                <el-option
                  v-for="item in dishesInfoList2"
                  :key="item.deviceModel"
                  :value="item.deviceId"
                  :label="item.deviceModel"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="5">
            <el-form-item>
              <div class="sub-title">检测设备：主机</div>
              <el-select
                v-model="defaultForms.beizhu25"
                placeholder="选择主机"
                clearable
                style="width: 170px;"
                @focus="handleQueryZhuji"
              >
                <el-option
                  v-for="item in dishesInfoList3"
                  :key="item.deviceModel"
                  :value="item.deviceId"
                  :label="item.deviceModel"
                />
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <div>
            <el-divider>确认检测计划</el-divider>
          </div>
        </el-row>
        <el-row>
          <el-container>
            <el-col :span="10">
              <el-form-item>
                <el-aside width="200px" align="center">确认意见</el-aside>
              </el-form-item>
            </el-col>
            <el-col>
              <el-form-item>
                <el-row>
                  施工单位负责人意见： 无
                </el-row>
              </el-form-item>
              <el-form-item>
                <el-row>
                  监理工程师意见： 无
                </el-row>
              </el-form-item>
              <el-form-item>
                <el-row>
                  现场检测人员意见： 无
                </el-row>
              </el-form-item>
            </el-col>
          </el-container>
        </el-row>
        <el-row>
          <el-container>
            <el-col :span="10">
              <el-form-item>
                <el-aside width="200px" align="center">确认检测时间</el-aside>
              </el-form-item>
            </el-col>
            <el-col>
              <el-form-item>
                <div>
                  <el-radio v-model="defaultForms.beizhu22" label="1" border>同意</el-radio>
                  <el-radio v-model="defaultForms.beizhu22" label="0" border>不同意</el-radio>
                </div>
              </el-form-item>
            </el-col>
          </el-container>
        </el-row>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button type="text" @click=" cancelDialog()">取消</el-button>
        <el-button v-permission="['admin','testInformation:jianceupdateTestInformation']" :loading="crud.status.cu === 2" type="primary" @click="submitDesForm(defaultForms)">提交报检单</el-button>
      </div>
    </el-dialog>
    <tunnel ref="openTunnel" />
  </div>
</template>

<script>
import store from '@/store'
import crudTestInformation from '@/api/system/testInformation'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'
import tunnel from './tunnel'
import { edit, createTest, editForm, delForm, listDishesInfo, listDishesInfo1, createErweima, listDishesInfoTianxian, listDishesInfoZhuji, jilieditForm, jianceeditForm } from '@/api/system/testInformation'
import { mapGetters } from 'vuex'
import { select, changeStatue, selectByStatueFenye, selectByStatue, selectByTunnelName } from '@/api/system/tunnelInformation'
import { getToken } from '@/utils/auth'
import { downloadFileRaw } from '@/utils/index'
import { generator } from '@/api/system/testInformation'
const baseUrl = process.env.VUE_APP_BASE_API === '/' ? '' : process.env.VUE_APP_BASE_API
const defaultForm = { testInforId: null, testId: null, testTime: null, testStartingDistance: null, testEndingDistance: null, testLength: null, wallRockType: null, supportTickness: null, separationDistance: null, meshDistance: null, annularBarDistance: null, reinforPrtTickness: null, secLineArchTickness: null, secLineWallTickness: null, secLineInverArchTickness: null, secLineFilerTickness: null, projectName: null, sectionName: null, tunnelName: null, worksiteName: null, statute: null, beizhu1: null, beizhu2: null, beizhu3: null, beizhu4: null, beizhu5: null, beizhu6: null, beizhu7: null, beizhu8: null, beizhu9: null, beizhu10: null, beizhu11: null, beizhu12: null, beizhu13: null, beizhu14: null, beizhu15: null }
export default {
  name: 'TestInformation',
  components: { tunnel, pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: 'api/testInformation', url: 'api/testInformation', idField: 'testInforId', sort: 'testInforId,desc', crudMethod: { ...crudTestInformation }})
  },
  data() {
    return {
      Str1: '初始化 - 施工单位',
      activities: [],
      activities1: [{
        content: '初始化 - 施工单位',
        timestamp: '',
        size: 'large',
        type: 'primary',
        icon: 'el-icon-more'
      }, {
        content: '发布提交审核 - 施工单位',
        timestamp: '',
        color: '#0bbd87'
      }, {
        content: '待审核 - 监理单位',
        timestamp: '',
        size: 'large',
        color: '#f67f01'
      }, {
        content: '待审核 - 检测单位',
        timestamp: '',
        color: '#f67f01'
      }],
      activities2: [{
        content: '初始化 - 施工单位',
        timestamp: '',
        size: 'large',
        type: 'primary',
        icon: 'el-icon-more'
      }, {
        content: '发布提交审核 - 施工单位',
        timestamp: '',
        color: '#0bbd87'
      }, {
        content: '已审核 - 监理单位',
        timestamp: '',
        size: 'large',
        color: '#0bbd87'
      }, {
        content: '待审核 - 检测单位',
        timestamp: '',
        color: '#f67f01'

      }],
      activities3: [{
        content: '初始化 - 施工单位',
        timestamp: '',
        size: 'large',
        type: 'primary',
        icon: 'el-icon-more'
      }, {
        content: '发布提交审核 - 施工单位',
        timestamp: '',
        color: '#0bbd87'
      }, {
        content: '已审核 - 监理单位',
        timestamp: '',
        size: 'large',
        color: '#0bbd87'
      }, {
        content: '已审核 - 检测单位',
        timestamp: '',
        color: '#0bbd87'
      }],
      defaultForms: {
        testInforId: null,
        testId: null,
        testTime: null,
        testStartingDistance: null,
        testEndingDistance: null,
        testLength: null,
        wallRockType: null,
        supportTickness: null,
        separationDistance: null,
        meshDistance: null,
        annularBarDistance: null,
        reinforPrtTickness: null,
        secLineArchTickness: null,
        secLineWallTickness: null,
        secLineInverArchTickness: null,
        secLineFilerTickness: null,
        projectName: null,
        sectionName: null,
        tunnelName: null,
        worksiteName: null,
        statute: null,
        beizhu1: null,
        beizhu2: null,
        beizhu3: null,
        beizhu4: null,
        beizhu5: null,
        beizhu6: null,
        beizhu7: null,
        beizhu8: null,
        beizhu9: null,
        beizhu10: null,
        beizhu11: null,
        beizhu12: null,
        beizhu13: null,
        beizhu14: null,
        beizhu15: null,
        beizhu16: null,
        beizhu17: null,
        beizhu18: null,
        beizhu19: null,
        beizhu20: null,
        beizhu21: null,
        beizhu22: null,
        beizhu23: null,
        beizhu24: null,
        beizhu25: null,
        beizhu26: null,
        beizhu27: null,
        beizhu28: null,
        beizhu29: null
      },
      dataid: -1,
      TestShenHeDialog: false,
      openTuneldialog: false,
      BaojianDialog: false,
      shigongdanweiShenHeDialog: false,
      jianlidanweishenheDialog: false,
      dialog: false,
      DataList: [],
      Data: [],
      DataForm: [],
      TunnelDialog: false,
      TunnelInfoDialog: false,
      updateDetectionSummaryPath: baseUrl + '/api/testInformation/updateBeiZhu26',
      uploadDetectionSummaryDialogIs: false,
      headers: { 'Authorization': getToken() },
      th: '',
      dishesInfoList: [],
      dishesInfoList1: [],
      dishesInfoList2: [],
      dishesInfoList3: [],
      options: [{
        value: '自检',
        label: '自检'
      }, {
        value: '第三方',
        label: '第三方'
      }],
      options1: [{
        value: '地质雷达法',
        label: '地质雷达法'
      }, {
        value: '瞬变电磁法',
        label: '瞬变电磁法'
      },
      {
        value: '其他',
        label: '其他'
      }],
      errorInfo: '', errordialog: false,
      permission: {
        add: ['admin', 'testInformation:add'],
        edit: ['admin', 'testInformation:edit'],
        del: ['admin', 'testInformation:del']
      },
      rules: {
        beizhu16: [
          { required: true, message: '待检区段起始里程不能为空', trigger: 'blur' }
        ],
        beizhu14: [
          { required: true, message: '待检区段起始里程不能为空', trigger: 'blur' }
        ],
        beizhu17: [
          { required: true, message: '待检区段起始里程不能为空', trigger: 'blur' }
        ],
        beizhu15: [
          { required: true, message: '待检区段起始里程不能为空', trigger: 'blur' }
        ],
        testLength: [
          { required: true, message: '待检区段长度不能为空', trigger: 'blur' }
        ],
        beizhu13: [
          { required: true, message: '检测时间不能为空', trigger: 'blur' }
        ]
      },
      queryTypeOptions: [
        { key: 'testInforId', display_name: 'ID' },
        { key: 'testId', display_name: '报检号' },
        { key: 'testTime', display_name: '申请检测时间' },
        { key: 'testStartingDistance', display_name: '待检区段起始里程' },
        { key: 'testEndingDistance', display_name: '待检区段结束里程' },
        { key: 'testLength', display_name: '待检区段长度' },
        { key: 'wallRockType', display_name: '围岩类型' },
        { key: 'supportTickness', display_name: '初支厚度' },
        { key: 'separationDistance', display_name: '间距(m/榀)' },
        { key: 'meshDistance', display_name: '钢筋网间距' },
        { key: 'annularBarDistance', display_name: '环向钢筋间距' },
        { key: 'reinforPrtTickness', display_name: '钢筋保护厚度' },
        { key: 'secLineArchTickness', display_name: '二次衬砌厚度-拱部' },
        { key: 'secLineWallTickness', display_name: '二次衬砌厚度-边墙' },
        { key: 'secLineInverArchTickness', display_name: '二次衬砌厚度-仰拱' },
        { key: 'secLineFilerTickness', display_name: '二次衬砌厚度-填充' },
        { key: 'projectName', display_name: '项目名称' },
        { key: 'sectionName', display_name: '标段名称' },
        { key: 'tunnelName', display_name: '隧道名称' },
        { key: 'worksiteName', display_name: '工点名称' },
        { key: 'statute', display_name: '状态' }

      ]
    }
  },
  computed: {
    ...mapGetters([
      'user',
      'baseApi',
      'fileUploadApi'
    ])
  },
  beforeCreate() {
    selectByStatue().then(response => {
      this.Data = response
    })
  },
  methods: {
    // 钩子：在获取表格数据之前执行，false 则代表不获取数据
    [CRUD.HOOK.beforeRefresh]() {
      return true
    },
    // 二维码
    createErweima(data) {
      if (data.statute === '报检单已审批') {
        createErweima(data).then(res => {
          this.errorInfo = res
          this.errordialog = true
        })
      } else {
        this.$confirm('报检单未完成审批,二维码不可用！！！')
      }
    },
    handleQuery() {
      listDishesInfo().then(response => {
        this.dishesInfoList = response
      })
    },
    handleQuery1() {
      listDishesInfo1().then(response => {
        this.dishesInfoList1 = response
      })
    },
    handleQueryTianxian() {
      listDishesInfoTianxian().then(response => {
        this.dishesInfoList2 = response
      })
    },
    handleQueryZhuji() {
      listDishesInfoZhuji().then(response => {
        this.dishesInfoList3 = response
      })
    },
    lookTunnelMess() {
      // this.$refs.openTunnel.dialog = true
      this.openTuneldialog = true
      this.crud.toQuery()
    },
    cancelCU() {
      this.BaojianDialog = false
      delForm(this.defaultForms.testInforId).then(response => {
      })
    },
    submitDeForm(formName) {
      jilieditForm(formName).then(response => {
        this.jianlidanweishenheDialog = false
        this.crud.toQuery()
        this.crud.notify('提交成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
      })
    },
    submitDesForm(formName) {
      jianceeditForm(formName).then(response => {
        this.TestShenHeDialog = false
        this.crud.toQuery()
        this.crud.notify('提交成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
      })
    },
    submitForm(formName) {
      editForm(formName).then(response => {
        this.BaojianDialog = false
        this.crud.toQuery()
        this.crud.notify('提交成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
      })
    },
    delmmess(formName) {
      if (formName.beizhu13 === null && formName.beizhu14 === null && formName.beizhu15 === null && formName.beizhu16 === null && formName.beizhu17 === null) {
        delForm(formName.testInforId).then(response => {
        })
      }
    },
    serach() {
      if (this.$refs.tunnelName.value.trim().length <= 0) {
        selectByStatue().then(response => {
          this.Data = response
        })
      } else {
        selectByTunnelName(this.$refs.tunnelName.value.trim()).then(response => {
          this.Data = response
        })
      }
    },
    createTest(data) {
      createTest(data).then(response => {
        this.defaultForms = response
        this.defaultForms.beizhu5 = this.user.nickName
        this.defaultForms.beizhu6 = this.user.username
        this.defaultForms.beizhu7 = this.user.phone
      })
      this.BaojianDialog = true
    },
    // 上传文件
    look(data) {
      select(data).then(response => {
        this.DataList = response
      })
      this.TunnelInfoDialog = true
    },
    cancelCUs() {
      this.TunnelDialog = false
      this.BaojianDialog = false
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
    cancelOpenTuneldialog() {
      this.crud.toQuery()
    },
    JianceCheck(data) {
      this.defaultForms = data
      if (data.statute === '检测单位待审批') {
        this.TestShenHeDialog = true
      } else if (data.statute === '报检单已审批') {
        this.$confirm('报检单已审批')
      } else {
        this.$confirm('等待监理单位待审批')
      }
    },
    JianliCheck(data) {
      this.defaultForms = data
      if (data.statute === '监理单位待审批') {
        if (data.beizhu19 === '1' && data.beizhu22 === '1') {
          this.activities3[0].timestamp = data.beizhu18
          this.activities3[1].timestamp = data.beizhu18
          this.activities3[2].timestamp = data.beizhu21
          this.activities3[3].timestamp = data.beizhu23
          this.activities = this.activities3
          this.jianlidanweishenheDialog = true
        } else if (data.beizhu19 === '1') {
          this.activities2[0].timestamp = data.beizhu18
          this.activities2[1].timestamp = data.beizhu18
          this.activities2[2].timestamp = data.beizhu21
          this.activities = this.activities2
          this.jianlidanweishenheDialog = true
        } else {
          this.activities1[0].timestamp = data.beizhu18
          this.activities1[1].timestamp = data.beizhu18
          this.activities = this.activities1
          this.jianlidanweishenheDialog = true
        }
      } else if (data.statute === '报检单已审批') {
        this.$confirm('报检单已审批')
      } else {
        this.$confirm('等待检测单位待审批')
      }
    },
    SigongCheck(data) {
      this.defaultForms = data
      if (data.beizhu19 === '1' && data.beizhu22 === '1') {
        this.activities3[0].timestamp = data.beizhu18
        this.activities3[1].timestamp = data.beizhu18
        this.activities3[2].timestamp = data.beizhu21
        this.activities3[3].timestamp = data.beizhu23
        this.activities = this.activities3
        this.shigongdanweiShenHeDialog = true
      } else if (data.beizhu19 === '1') {
        this.activities2[0].timestamp = data.beizhu18
        this.activities2[1].timestamp = data.beizhu18
        this.activities2[2].timestamp = data.beizhu21
        this.activities = this.activities2
        this.shigongdanweiShenHeDialog = true
      } else {
        this.activities1[0].timestamp = data.beizhu18
        this.activities1[1].timestamp = data.beizhu18
        this.activities = this.activities1
        this.shigongdanweiShenHeDialog = true
      }
    },
    cancelDialog() {
      this.shigongdanweiShenHeDialog = false
      this.jianlidanweishenheDialog = false
      this.TestShenHeDialog = false
    },
    updateDetectionSummaryDialog(data) {
      this.dataid = data.testInforId
      this.uploadDetectionSummaryDialogIs = true
    },
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
    // beforesubmit(response, file, fileList) {
    //   this.$refs.upload.clearFiles()
    // },
    handleSuccess(response, file, data) {
      // data.detectionPhotos = response.data
      // edit(data)
      this.crud.notify('上传成功', CRUD.NOTIFICATION_TYPE.SUCCESS)
      // this.changeVersion(response, 1)
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
    cancel() {
      this.uploadPhotoDialog = false
    },
    downloadDetectionSummary(data, name) {
      // 打包下载
      generator(data, -2).then(data => {
        downloadFileRaw(data, name)
      })
    }
  }
}
</script>

<style scoped>

</style>

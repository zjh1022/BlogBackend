<template>
  <div class="app-container">
    <el-form :inline="true" label-width="68px">
      <el-form-item label="ip地址">
        <el-input v-model="queryParams.ip" placeholder="请输入ip地址" clearable style="width: 240px;" size="small"
                  @keyup.enter.native="handleQuery"/>
      </el-form-item>
      <el-form-item label="访问地点">
        <el-input v-model="queryParams.location" placeholder="请输入访问地点" clearable style="width: 240px;" size="small"
                  @keyup.enter.native="handleQuery"/>
      </el-form-item>
<!--  -->
      <el-form-item label="访问时间">
        <el-date-picker v-model="dateRange" size="small" style="width: 240px" value-format="yyyy-MM-dd" type="daterange"
                        range-separator="-" start-placeholder="开始日期" end-placeholder="结束日期"/>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" icon="el-icon-search" size="mini" @click="handleQuery">搜索</el-button>
        <el-button icon="el-icon-refresh" size="mini" @click="resetQuery">重置</el-button>
      </el-form-item>
    </el-form>

    <el-row :gutter="10" class="mb8">
      <el-col :span="1.5">
        <el-button type="danger" icon="el-icon-delete" size="mini" :loading="delLoading" :disabled="multiple"
                   @click="handleDelete">删除
        </el-button>
      </el-col>
      <el-col :span="1.5">
        <el-button type="danger" icon="el-icon-delete" size="mini" :loading="delLoading"
                   @click="handleClean">清空
        </el-button>
      </el-col>

    </el-row>

    <el-table v-loading="loading" :data="list" @selection-change="handleSelectionChange">
      <el-table-column type="selection"/>
      <el-table-column label="IP" prop="ip" :show-overflow-tooltip="true"/>
      <el-table-column label="访问地点" prop="location"/>
      <el-table-column label="浏览器" prop="browser"/>
      <el-table-column label="操作系统" prop="os"/>

      <el-table-column label="访问时间" prop="createTime" width="180">
        <template slot-scope="scope">
          <span>{{ parseTime(scope.row.createTime) }}</span>
        </template>
      </el-table-column>>
    </el-table>

    <pagination
      v-show="total>0" :total="total" :page.sync="queryParams.pageNum" :limit.sync="queryParams.pageSize"
      @pagination="init"/>
  </div>
</template>

<script>

  import initData from '@/mixins/initData'

  export default {
    mixins: [initData],
    data() {
      return {
        // 状态数据字典
        statusOptions: [],
        // 查询参数
        queryParams: {
          ip: undefined,
          location: undefined,
          status: undefined
        }
      };
    },
    created() {
      this.$nextTick(() => {
        this.init()
      })
    },
    methods: {
      beforeInit() {
        this.base = '/log/visitLog';
        this.modelName = '访问日志';
        return true
      },
    }
  };
</script>


<template>
  <!--
  主显：姓名  所属公司  联系方式

  姓名：张三      所属公司：德邦快递
  工号：xxx      所属部门：xx部门
  职位：主管      联系方式：18888888888
  公司地址：xxx
  -->
  <div class="tableContain">

    <div class="query-line">
      <el-form :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="姓名">
          <el-input v-model="formInline.name" placeholder="请输入司机姓名"></el-input>
        </el-form-item>
        <el-form-item label="公司名称">
          <el-input v-model="formInline.company" placeholder="请输入车牌号"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary">查询</el-button>
        </el-form-item>
      </el-form>

    </div>

    <div class="table">
      <el-table
          :data="filData"
          style="width: 100%">
        <el-table-column type="expand">
          <template slot-scope="props">
            <el-form label-position="left" inline class="demo-table-expand">
              <el-form-item label="工号">
                <span>{{ props.row.id }}</span>
              </el-form-item>
              <el-form-item label="姓名">
                <span>{{ props.row.name }}</span>
              </el-form-item>
              <el-form-item label="所属公司">
                <span>{{ props.row.company }}</span>
              </el-form-item>
              <el-form-item label="所属部门">
                <span>{{ props.row.depart }}</span>
              </el-form-item>
              <el-form-item label="职位">
                <span>{{ props.row.job }}</span>
              </el-form-item>
              <el-form-item label="公司地址">
                <span>{{ props.row.address }}</span>
              </el-form-item>
              <el-form-item label="联系方式">
                <span>{{ props.row.telephone }}</span>
              </el-form-item>
            </el-form>
          </template>
        </el-table-column>
        <el-table-column
            label="姓名"
            width="240"
            prop="name">
        </el-table-column>
        <el-table-column
            label="公司名称"
            width="240"
            prop="company">
        </el-table-column>
        <el-table-column
            label="所属部门"
            width="240"
            prop="depart">
        </el-table-column>
        <el-table-column
            label="联系方式"
            width="240"
            prop="telephone">
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
export default {
  name: "ExpressContactView",
  data() {
    return {
      formInline: {
        name: '',
        company: ''
      },
      tableData: [{
        id: '120006',
        name: '张三',
        job: '主管',
        company: '德邦快递',
        address: '上海市普陀区真北路',
        depart: '运输部',
        telephone: '18887887887'
      }, {
        id: '120008',
        name: '李四',
        job: '主管',
        company: '中通快递',
        address: '上海市普陀区真北路',
        depart: '运输部',
        telephone: '18889587887'
      }, {
        id: '120018',
        name: '王五',
        job: '主管',
        company: '圆通快递',
        address: '上海市普陀区真北路',
        depart: '运输部',
        telephone: '18048887887'
      }, {
        id: '120087',
        name: '李以亦',
        job: '主管',
        company: '申通快递',
        address: '上海市普陀区真北路',
        depart: '运输部',
        telephone: '18888587887'
      }, {
        id: '120548',
        name: '张紫山',
        job: '主管',
        company: '顺丰快递',
        address: '上海市普陀区真北路',
        depart: '运输部',
        telephone: '18688887887'
      },
        {
          id: '120575',
          name: '千山',
          job: '主管',
          company: '京东物流',
          address: '上海市普陀区真北路',
          depart: '运输部',
          telephone: '18686887887'
        }]
    }
  },
  methods: {},
  computed: {
    filData() {
      return this.tableData.filter((d) => {
        return d.name.indexOf(this.formInline.name) !== -1 && d.company.indexOf(this.formInline.company) !== -1
      })
    }
  }
}
</script>

<style scoped>
.demo-table-expand {
  font-size: 0;
}

.demo-table-expand label {
  width: 90px;
  color: #99a9bf;
}

.demo-table-expand .el-form-item {
  margin-right: 0;
  margin-bottom: 0;
  width: 50%;
}

/deep/ .demo-table-expand[data-v-e885dae2] {
  padding-left: 60px;
}

.query-line {
  display: flex;
  justify-content: center;
  width: 100%;
}

.tableContain {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;
  margin-bottom: 10px;
  flex-wrap: wrap;
}

.table {
  /*width: 80%;*/
  border: 1px solid aliceblue;
}
</style>
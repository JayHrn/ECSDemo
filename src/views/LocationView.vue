<template>

  <div class="tableContain">
    <div class="query-line">
      <el-form :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="司机姓名">
          <el-input v-model="formInline.driver" placeholder="请输入司机姓名"></el-input>
        </el-form-item>
        <el-form-item label="车牌号">
          <el-input v-model="formInline.plate" placeholder="请输入车牌号"></el-input>
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
        <el-table-column
            prop="date"
            label="车牌号"
            width="180">
        </el-table-column>
        <el-table-column label="配送信息">
          <el-table-column
              prop="name"
              label="姓名"
              width="150">
          </el-table-column>
          <el-table-column label="当前地址">
            <el-table-column
                prop="province"
                label="省份"
                width="150">
            </el-table-column>
            <el-table-column
                prop="city"
                label="市区"
                width="150">
            </el-table-column>
            <el-table-column
                prop="address"
                label="地址"
                width="360">
            </el-table-column>
          </el-table-column>
        </el-table-column>
      </el-table>
    </div>

  </div>

</template>

<script>
export default {
  name: "LocationView",
  data() {
    return {
      formInline: {
        driver: '',
        plate: ''
      },
      tableData: [{
        date: '赣A•A1101',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
        date: '赣A•A1102',
        name: '张三',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
        date: '赣A•A1103',
        name: '李四',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
        date: '赣A•A1104',
        name: '千琴一',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
        date: '赣A•A1105',
        name: '张紫山',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
        date: '赣A•A1106',
        name: '王小虎',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
        date: '赣A•A1107',
        name: '李以亦',
        province: '上海',
        city: '普陀区',
        address: '上海市普陀区金沙江路 1518 弄',
      }, {
          date: '赣A•A1108',
          name: '艺鸣',
          province: '上海',
          city: '普陀区',
          address: '上海市普陀区金沙江路 1518 弄',
        }]
    }
  },
  methods: {
    query() {
      console.log('submit!');
    }
  },
  computed: {
    filData() {
      return this.tableData.filter((d) => {
        return d.name.indexOf(this.formInline.driver) !== -1 && d.date.indexOf(this.formInline.plate) !== -1
      })
    }
  }
}
</script>

<style scoped>
.tableContain {
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: stretch;
  flex-wrap: wrap;
  flex-direction: row;
  margin-top: 10px;
}
.query-line{
  display: flex;
  justify-content: center;
  width: 100%;
}
</style>
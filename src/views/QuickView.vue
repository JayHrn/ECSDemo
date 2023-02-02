


<template>

    <div class="tableContain">
      <div class="query-line">
        <el-form :inline="true" :model="formInline" class="demo-form-inline">
          <el-form-item label="单号">
            <el-input v-model="formInline.no" placeholder="请输入货物单号"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary">查询</el-button>
          </el-form-item>
        </el-form>
      </div>
  
      <div class="table">
        <el-table
      ref="multipleTable"
      :data="tableData"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange">
          <el-table-column
          type="selection"
              width="55">
          </el-table-column>
        width="55">
          <el-table-column label="订单信息">
            <el-table-column
                prop="im"
                label="商品"
                width="150">
                <template slot-scope="scope">
                    <img :src="scope.row.im"/>
                </template>
            </el-table-column>
            <el-table-column
                prop="no"
                label="订单单号"
                width="200">
                
            </el-table-column>
            <el-table-column
                prop="name"
                label="商品名"
                width="200">
                
            </el-table-column>
            
              <el-table-column
                  prop="price"
                  label="单价"
                  width="100">
              </el-table-column>
              <el-table-column
                  prop="number"
                  label="数量"
                  width="50">
              </el-table-column>
              <el-table-column
                  prop="status"
                  label="交易状态"
                  width="100">
              </el-table-column>
              <el-table-column
                  label="交易操作"
                  width="100">
                    <el-button
                    type="danger"
                    size="mini"
                    @click="quick()">加急服务</el-button>
                    
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
          num: ''
        },
        tableData: [{
          no:'No111',
          im:'https://gw.alicdn.com/imgextra/i2/2208356464114/O1CN019Yd6JR1gGG5og9pQE_!!2208356464114.jpg_110x10000Q75.jpg_.webp',
          name:'便签本 可撕无粘性ins风任务清单 [交易快照]',
          price: '￥4.80',
          number: '1',
          status: '退款/退换货/投诉',
        },
        {
            no:'No222',
        im:'https://gw.alicdn.com/imgextra/i2/743905254/O1CN01mRznF81ogNjmzeu2v_!!743905254.jpg_110x10000Q75.jpg_.webp',
          name:'魔女限定斑马中性笔JJ15 [交易快照]',
          price: '￥7.80',
          number: '1',
          status: '退款/退换货/投诉',
        },
        {
            no:'No333',
            im:'https://gd1.alicdn.com/imgextra/i1/195771728/O1CN01CJAquu1OdT7JKLdgc_!!195771728.jpg_50x50.jpg_.webp',
          name:'斑马进口日本速干学生考试中性笔 [交易快照]',
          price: '￥16.80',
          number: '1',
          status: '退款/退换货/投诉',
        }]
      }
    },
    methods: {
        quick(){
            this.$message({
          message: '恭喜你，加急服务设置成功',
          type: 'success'
        });
        },
        
      query() {
        console.log('submit!');
      }
    },
    computed: {
      filData() {
        return this.tableData.filter((d) => {
          return d.name.indexOf(this.formInline.no) !== -1 
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
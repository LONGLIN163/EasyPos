<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
          <el-tabs v-model="activeName" @tab-click="handleClick">
            <el-tab-pane label="Order">

              <el-table 
                :data="tableData" 
                border 
                style="width:100%"
              > 
                  <el-table-column prop="articleName" label="Article"></el-table-column>
                  <el-table-column prop="quantity" label="Quantity" width="80"></el-table-column>
                  <el-table-column prop="price" label="Price" width="70"></el-table-column>
                  <el-table-column label="action" width="100" fixed="right">
                    <template slot-scope>
                      <el-button type="text" size="small">Add</el-button>
                      <el-button type="text" size="small">Min</el-button>
                    </template>
                  </el-table-column>
              </el-table>
              <div class="order-status">
                <el-button type="warning">Pending</el-button>
                <el-button type="danger">Del</el-button>
                <el-button type="success">Check out</el-button>
              </div>

            </el-tab-pane>
            <el-tab-pane label="Pending" name="second">配置管理</el-tab-pane>
            <el-tab-pane label="Delievery" name="third">角色管理</el-tab-pane> 
          </el-tabs>
      </el-col>
      <el-col>
        Articles
      </el-col>
    </el-row>
   
  </div>
</template>

<script>
//import leftNav from "@/components/common/leftNav.vue"
export default {
  name: 'pos',
  data(){
    return {
      tableData:[{
        articleName: 'xixi',
        price: 8,
        quantity:1
      }, {
        articleName: 'haha',
        price: 15,
        quantity:1
      }, {
        articleName: 'hehe',
        price: 8,
        quantity:1
      }, {
        articleName: 'hehe',
        price: 8,
        quantity:1
      }]
    }
  },
  mounted:function(){
    var orderHeight=document.body.clientHeight;
    console.log(orderHeight)
    document.getElementById("order-list").style.height=orderHeight+'px';
  }
}
</script>

<style scoped>
.pos-order{
  background-color: rgb(226, 225, 218);
  border-right: 1px solid skyblue;
  /* height: 100% !important; */
}
.order-status{
  margin-top: 10px;
}

</style>

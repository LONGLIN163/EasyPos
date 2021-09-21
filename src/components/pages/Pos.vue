<template>
  <div class="pos">
    <el-row>
      <el-col :span='7' class="pos-order" id="order-list">
        Orders
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
          msg:"haha"
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
  background-color: white;
  border-right: 1px solid skyblue;
  /* height: 100% !important; */
}

</style>

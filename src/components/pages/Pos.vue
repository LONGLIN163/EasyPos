<template>
  <div class="pos">
    <div>
      <el-row>
        <el-col :span='7' class="pos-order" id="order-list">
            <el-tabs stretch>
              <el-tab-pane label="Order">

                <el-table 
                  :data="tableData"
                  show-summary 
                  border 
                  style="width:100%"
                > 
                    <el-table-column prop="articleName" label="Article"></el-table-column>
                    <el-table-column prop="quantity" label="Quantity" width="80"></el-table-column>
                    <el-table-column prop="price" label="Price" width="70"></el-table-column>
                    <el-table-column label="action" width="100" fixed="right">
                      <template slot-scope="scope">
                        <el-button type="text" size="small" @click="addOrderList(scope.row)">Add</el-button>
                        <el-button type="text" size="small">Min</el-button>
                      </template>
                    </el-table-column>
                </el-table>
                <div class="totalDiv">
                  <small>Amount:</small>{{totalQuantity}} &nbsp;&nbsp;&nbsp; <small>Total:</small>{{totalPrice}}€
                </div>
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
        <el-col :span='17'>
            <div class="hot-sells">
              <div class="title">Hot Sell</div>
              <div class="hot-sells-list">
                  <ul>
                      <li v-for="item in hotSells" :key="item.id" @click="addOrderList(item)">
                        <span>{{item.articleName}}</span>
                        <span class="hot-price">{{item.price}}€</span>
                      </li>
                  </ul>
              </div>
            </div>
          <div class="article-type">
            <el-tabs stretch>

              <el-tab-pane label="Salad">
                <div>
                  <ul class='cookList'>
                      <li v-for="item in type0Articles" :key="item.articleId" @click="addOrderList(item)">
                          <span class="foodImg">
                            <img :src="item.articleImg" width="100%">
                          </span>
                          <span class="foodName">
                            <p>
                              {{item.articleName}}
                            </p>
                            <p class="foodPrice">{{item.price}}€</p>
                          </span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="Menu">
                <div>
                  <ul class='cookList'>
                      <li v-for="item in type1Articles" :key="item.articleId" @click="addOrderList(item)">
                          <span class="foodImg">
                            <img :src="item.articleImg" width="100%">
                          </span>
                          <span class="foodName">
                            <p>
                              {{item.articleName}}
                            </p>
                            <p class="foodPrice">{{item.price}}€</p>
                          </span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="Drinks">
                <div>
                  <ul class='cookList'>
                      <li v-for="item in type2Articles" :key="item.articleId" @click="addOrderList(item)">
                          <span class="foodImg">
                            <img :src="item.articleImg" width="100%">
                          </span>
                          <span class="foodName">
                            <p>
                              {{item.articleName}}
                            </p>
                            <p class="foodPrice">{{item.price}}€</p>
                          </span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>
              <el-tab-pane label="Pastries">
                <div>
                  <ul class='cookList'>
                      <li v-for="item in type3Articles" :key="item.articleId" @click="addOrderList(item)">
                          <span class="foodImg">
                            <img :src="item.articleImg" width="100%">
                          </span>
                          <span class="foodName">
                            <p>
                              {{item.articleName}}
                            </p>
                            <p class="foodPrice">{{item.price}}€</p>
                          </span>
                      </li>
                  </ul>
                </div>
              </el-tab-pane>

            </el-tabs>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
//import leftNav from "@/components/common/leftNav.vue"
import axios from "axios"
import fakeData2 from "../../assets/data/fakeData2.js"
 
export default {
  name: 'pos',
  data(){
    return {
      tableData:[],
      hotSells:[],
      type0Articles:[],
      type1Articles:[],
      type2Articles:[],
      type3Articles:[],
      totalQuantity:0,
      totalPrice:0
    }
  },
  created:function(){
    // ******get hot sell product******
    axios.get('https://mocki.io/v1/2ad1210f-5e1f-4cf0-b855-93250112feb4')
    .then( (res) => {
      this.hotSells=res.data.data;
       //console.log(this.hotSells)
    })
    .catch( (err) => {
      alert("Request data failed, Internet error!")
    })
    // ******get type0Articles product******
    // ******mocki can not handles complex api, use local fake data ******
    //console.log(fakeData2)
    this.type0Articles=fakeData2[0]
    this.type1Articles=fakeData2[1]
    this.type2Articles=fakeData2[2]
    this.type3Articles=fakeData2[3]

  },
  mounted:function(){
    var orderHeight=document.body.clientHeight;
    console.log(orderHeight)
    document.getElementById("order-list").style.height=orderHeight+'px';
  },
  methods:{
          addOrderList(articleObj){
            this.totalQuantity=0; 
            this.totalPrice=0;
            let isHas=false;
            for (let i=0; i<this.tableData.length;i++){
                console.log(this.tableData[i].articleId);
                if(this.tableData[i].articleId==articleObj.articleId){
                    isHas=true; 
                }
            }
            if(isHas){
                 let arr = this.tableData.filter(o =>o.articleId == articleObj.articleId);
                 arr[0].quantity++;
                 console.log(arr); 
            }else{
                let newArticle={
                  articleId:articleObj.articleId,
                  articleName:articleObj.articleName,
                  price:articleObj.price,
                  quantity:1
                };
                this.tableData.push(newArticle);
            }

            this.tableData.forEach((element) => {
                this.totalQuantity+=element.quantity;
                this.totalPrice=this.totalPrice+(element.price*element.quantity);   
            });

      }

  }
}
</script>

<style scoped>
.pos-order{
  background-color: #F9FAFC;
  border-right: 1px solid skyblue;
  /* height: 100% !important; */
}

.order-status{
  margin-top: 10px;
}
 .title{
  height: 20px;
  border-bottom:1px solid #D3DCE6;
  background-color: #F9FAFC;
  padding:10px;
}
.totalDiv{
  background-color: #fff;
  padding: 10px;
  border-bottom: 1px solid #D3DCE6;
}
.hot-sells ul li{
  list-style: none;
  float:left;
  border:1px solid #E5E9F2;
  padding:10px;
  margin:5px;
  background-color:#fff;
  cursor: pointer;
}
.hot-price{
  color:#58B7FF; 
}
.article-type{
  clear: both;
}
.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
       cursor: pointer;

   }
   .cookList li span{
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       text-align: center;
       color:brown;
       width: 60%;

   }
   .foodPrice{
       display: block;
       text-align: center;
       font-size: 14px;
       padding-top:0px;
       color:rgb(0, 0, 0);

   }

</style>

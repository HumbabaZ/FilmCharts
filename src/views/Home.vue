<template>
<div>
  <div class="header" :style="header" style="padding-top:280px;">
    <h3 style="font-size:30px;padding-left:60px;color:#303133;background-color:#fff;margin:0 200px;padding-top:80px;padding-bottom:40px;border-radius:8px 8px 0 0 ;">
      电影列表
      </h3>
  </div>
  <div class="home" style="height:100%;background-color:#F5F5F5;padding:0 200px;padding-bottom:60px;">
    
    <div class="main" style="background-color:#fff;padding:40px 30px;border:qpx solid #ddd;border-radius:0 0 8px 8px;">
      

      <el-table
        :data="filmData.slice((currentPage-1)*pagesize,currentPage*pagesize)"
        style="width: 100%"
        empty-text="暂无数据"
        @row-click="handle"
        >
        <el-table-column
          label=""
          width="180">
          <template slot-scope="scope">
            <img :src="scope.row.poster" width="90" height="120" class="poster" alt="暂无海报"/>
          </template>
        </el-table-column>
        <el-table-column
          prop="title"
          label="电影名称"
          width="330"
          >
        </el-table-column>
        <el-table-column
          prop="rating.average"
          label="评分"
          width="50">
        </el-table-column>
        <el-table-column
          prop="genres"
          label="类型"
          width="100">
        </el-table-column>
        <el-table-column
          label="演员"
          width="250">
          <template slot-scope="scope">
            <span>{{castList(scope.row.casts)}}</span>
          </template>
        </el-table-column>
        <el-table-column
          prop="directors[0].name"
          label="导演"
          width="140">
        </el-table-column>
      </el-table>
      
      <div class="pageContainer" style="text-align: center;margin-top:30px">
        <el-pagination
        :pager-count="11"
        layout="prev, pager, next"
        :total="total"
        @current-change="current_change"
        >
      </el-pagination>
      </div>
      
     
   </div>
  </div>
</div>
</template>

<script>
import filmData from '@/components/films.json'

export default {
  name: 'home',
  data(){
    return{
      filmData:filmData,
      pagesize:10,
      total:filmData.length, 
      currentPage:1,
      castlist:'',
      header: {
          backgroundImage: "url(" + require("../assets/banner.jpg") + ") ",
          backgroundPosition: "center center",
          backgroundRepeat: "no-repeat",
          backgroundSize: "cover",
          
        },
    }
  },
  methods:{
    current_change:function(currentPage){
        this.currentPage = currentPage;
      },
    castList(scope){
      var arr=[];
      for(let i=0;i<scope.length;i++){
        if(scope[i].name==null){
          arr.push("暂无数据");
        }
        else{
          arr.push(scope[i].name);
        }
      }
      return arr.toString();
    },
    handle(row, event, column){
      //console.log(row, event, column)
      this.$router.push({
          name: 'details',
          params: {
            data:row
          }
        })
    }
  },
  mounted(){
    
  },
  computed:{
    
  }
}
</script>

<style>
.home .el-table__body tr{
height:150px;
}
</style>


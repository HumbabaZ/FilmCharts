<template>
<div>
  <div class="header" :style="header" style="padding-top:280px;">
    <div style="font-size:30px;padding-left:60px;color:#303133;background-color:#fff;margin:0 200px;padding-top:80px;height:150px;border-radius:8px 8px 0 0 ;">
      <h3 style="width:50%;">{{data.title}}（{{data.year}}）</h3>
      </div>
  </div>
  <div class="detail" style="height:100%;background-color:#F5F5F5;padding:0 200px;padding-bottom:60px;">
    
    <div class="main" style="background-color:#fff;padding:0 30px 40px 30px;border:qpx solid #ddd;border-radius:0 0 8px 8px;">
      <el-row style="min-height:300px;">
        <el-col :span="8">
            <img :src="data.poster" class="poster" alt="暂无海报" style="min-height:300px;"/>
        </el-col>
        <el-col :span="16">
            <div style="padding-left:30px;padding-top:30px">
                <p><b>别名：</b>{{deal(data.aka)}} </p>
                <p><b>语言：</b>{{deal(data.languages)}} </p>
                <p><b>国家：</b>{{deal(data.countries)}} </p>
                <p><b>类型：</b>{{deal(data.genres)}} </p>
                <p><b>上映时间：</b>{{deal(data.pubdate)}} </p>
                <p><b>时长:</b>{{deal(data.duration)}} 分钟 </p>
                <p><b>评分:</b>{{deal(data.rating.average)}} </p>
            </div>
        </el-col>
      </el-row>

      <el-row>
        <div class="info2" style="padding:30px 50px;">
          <p>
            <b>剧情简介：</b><br>{{deal(data.summary)}} 
          </p>
          <p><b>导演：</b>{{deal(data.writers[0].name)}}</p>  
          <p><b>演员：</b>{{deal(castList(data.casts))}}</p>  
        </div>
      </el-row>

      
   </div>
  </div>
</div>
</template>

<script>

export default {
  name: 'home',
  data(){
    return{
        data:this.$route.params.data,
        pagesize:10,
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
    deal(info){
      //console.log("info",info,this.data.aka);
      // result= (info!=null?info.toString():"暂无数据");
      // return result;
      if(info==""||info==null){
        return "暂无数据"
      }
     else {
      return info.toString()
     }
    }
  },
  mounted(){
    //console.log("params",this.$route.params.data)
  },
  computed:{
    filmData(){

    }
  }
}
</script>

<style>
.detail p{
    font-size:18px;
}
.info2 p{
  line-height: 35px
}
</style>


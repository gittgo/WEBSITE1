<template>
  <div class="footer" ref="footer">
    <div class="container " style="padding-bottom: 24px">
      <div class="content cl">
        <div class="footer-con1 fl">
          <el-col :span="24"><div class="grid-content bg-purple"><div class="title">战略合作</div></div></el-col>
          <div class="img-box cl" v-if="data2" >
            <div  v-for="item in data2"
                  class="footer-con1-imgbox fl"
                  :key="item.id">
              <img :src='item.image'
                   class="img"
                   @click="goNewUrl(item.jumpType,item.jumpUrl,item.jumpNewsId)">
            </div>
          </div>
        </div>
        <div class="footer-con2 fl">
          <el-col :span="24"><div class="grid-content bg-purple"><div class="title">合作内容</div></div></el-col>
          <div class="img-box cl" v-if="data1" >
            <div  v-for="(item,index) in data1"
                  class="footer-con2-imgbox fl"
                  :key="item.id">
              <img :src='item.image'
                   class="img"
                   @click="goNewUrl(item.jumpType,item.jumpUrl,item.jumpNewsId)">
            </div>
          </div>
        </div>
      </div>
      <div class="friendship">
        <span>友情链接:</span>&nbsp;&nbsp;&nbsp;
        <a href="https://www.binance.net" target="_blank">币安</a>&nbsp;&nbsp;
        <a href="https://www.mxc.com" target="_blank">抹茶</a>&nbsp;&nbsp;
        <a href="https://www.okex.com" target="_blank">OKEX</a>&nbsp;&nbsp;
        <a href="https://www.coldlar.com" target="_blank">酷神钱包</a>&nbsp;&nbsp;
        <a href="https://www.tuoniaox.com" target="_blank">鸵鸟区块链</a>&nbsp;&nbsp;
        <a href="https://www.bishijie.com" target="_blank">币世界</a>&nbsp;&nbsp;
        <a href="https://www.8btc.com" target="_blank">巴比特</a>&nbsp;&nbsp;
        <a href="http://bcsky.pro" target="_blank">链天下</a>&nbsp;&nbsp;
        <a href="https://www.chainfor.com" target="_blank">链向财经</a>
      </div>
      <div class="line"></div>
      <div class="bottom cl">
        <div class="fl small item-left text-left">
          Copyright &copy; 果味财经 版权所有 京ICP备17013792号-2
        </div>
        <div class="rt text-right about item-right">
          <router-link @click.native="scrolls" :to="{name:'about',params:{titleName:'aboutUs'}}" class="small"><span>关于我们</span></router-link>
          <router-link @click.native="scrolls" :to="{name:'about',params:{titleName:'contactUs'}}" class="small"><span>联系我们</span></router-link>
          <router-link @click.native="scrolls" :to="{name:'about',params:{titleName:'joinUs'}}" class="small"><span>加入我们</span></router-link>
          <router-link @click.native="scrolls" :to="{name:'about',params:{titleName:'copyrightNotice'}}" class="small"><span style="border-right: none">版权声明</span></router-link>
        </div>
      </div>
      <div style="clear: both"></div>
    </div>
  </div>
</template>

<script>
  import API from '../../assets/js/api'
  export default {
    name: "footerGuo",
    data(){
      return{
        cooperationContent:API.api.cfg.cooperationContent,
        strategicCooperation:API.api.cfg.strategicCooperation,
        data1:null,
        data2:null,
      }
    },
    methods:{
      getDatas:function () {
        let _this = this
        let params = {
          pageCurrent:1,
          pageSize:100,
        };
        _this.getData(_this.cooperationContent,params,function (res) {
          if(res.code===0){
            _this.data1=res.object
          }
        });
        _this.getData(_this.strategicCooperation,params,function (res) {
          if(res.code===0){
            _this.data2=res.object
          }
        })
      },
      scrolls:function () {
        window.scrollTo(0,0);
      }
    },
    mounted(){
      this.getDatas()
    }
  }
</script>

<style scoped>
  .footer{
    font-size: 20px;
    color: #ddd;
    /*width: 100%;*/
    background-color: #333333;
    clear: both;
  }
  .test{
    margin-right:3%;
  }
  .test1{
    margin-right: 9%;
  }
  .title{
    margin-top: 40px;
    margin-bottom: 46px;
    text-align: left;
    color: #ddd;
    vertical-align: middle;
  }
  .footer-con2 .img-box{
    /*display: flex;*/
    /*flex-direction: row;*/
    /*justify-content: space-between;*/
    /*align-items: center;*/

  }
  .img-box img{
    /*margin-right: 32px;*/
    /*margin-bottom: 21px;*/
    cursor: pointer;
    float: left;
    opacity: 0.5;
  }
  .img-box img:hover{
    opacity: 1;
  }
  .line{
    width: 100%;
    height: 1px;
    background-color: rgba(153, 153, 153,1);
    opacity: 0.17;
    margin:33px 0 20px 0;
  }
  .bottom{
    line-height: 14px;
    clear: both;
  }
  .small{
    font-size: 14px;
    color: #999;
  }
  .about span{
    border-right: 2px solid rgba(153, 153, 153, 0.17);
    padding: 0 10px;
    cursor: pointer;
  }
  .small span:hover{
    color: #fffefe;
  }
  .footer-con1-img{
    width: 108px;height: 38px;
  }
  /*.grid-content bg-purple img:hover{*/
    /*opacity: 1;*/
   /*}*/
  .footer-con1{
    width: 541px;
    /*margin-right: 159px;*/
  }
  .footer-con2{
    width: 659px;
  }
  .footer-con1-imgbox{
    width: 98px;
    height: 46px;
    overflow: hidden;
    margin-bottom: 28px;
    margin-right: 42px;
  }
  .footer-con2  .img-box>div:last-child{
    margin:0;
  }
  /*.footer-con1-imgbox:nth-child(even){*/
    /*margin:0 48px;*/
  /*}*/
  .footer-con2-imgbox{
    width: 98px;
    height: 46px;
    overflow: hidden;
    margin-bottom: 28px;
    margin-right: 42px;
    float: left;
  }
  .container{
    background-color: #333;
  }
  @media screen and (max-width: 500px) {
    .footer-con1{
      width :100%;
    }
    .footer-con2{
      width: 100%;
    }
    .small{
      text-align: center;
    }
    .about span{
      padding: 0 5px;
    }
  }


.friendship{
  color: #999;
  text-align: left;
  font-size: 14px;
  line-height: 20px;
}
.friendship a{
  color: #999;
  font-size: 14px;
}
</style>

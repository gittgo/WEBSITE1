<template>
    <div class="expressDetails container cl">
         <!-- <el-breadcrumb separator-class="el-icon-arrow-right"
                   style="font-size: 12px;margin: 20px 0 40px 0;padding: 0;">
            <el-breadcrumb-item v-if="parentType" style="color: #666">{{parentType}} > </el-breadcrumb-item>
            <el-breadcrumb-item style="color: #666">  7×24小时快讯详情</el-breadcrumb-item>
        </el-breadcrumb> -->
        <!-- 左 -->
        <div class="f_content fl">
            <div class="clock">
                <div class="month">
                    <div style="height:8px;width:100%;"> </div>
                    <span class="day">{{day}}</span><br>
                    <span class="day1">{{month}}月</span>
                </div>
                <div class="time">
                    <div class="week">{{detailsData.week}}</div>
                    <div class="week1">{{time}}</div>
                </div>
            </div>
            <div class="textdetails">
                <h1 class="title">{{detailsData.title}}</h1>
                <h2 class="text1">{{detailsData.mainText}}</h2>
            </div>
            <div class="goodbad">
                <p class="fr">
                    <img src="../../../src/assets/images/topHand1.png" alt="">
                    <span>利好</span>
                    <span>{{detailsData.good}}</span>
                </p>
                <p class="fr">
                    <img src="../../../src/assets/images/botHand1.png" alt="">
                    <span>利空</span>
                    <span>{{detailsData.bad}}</span>
                </p>
            </div>
            <div class="hint">本文由入驻果味财经的作者撰写，观点仅代表作者本人，绝对不代表果味财经赞同其观点或证实其描述。</div>
        </div>
        <!-- 右 -->
         <div class="rt left-con" :style="{marginTop:marginTop+'px'}"  >
            <div  class="img1"
                    v-for="(item,index) in rightAd"
                    :key="index"
                    v-if="index <= 2"
                    :class="!item?'border-line':null">
                <img :src='item.image'
                    v-if="item"
                    @click="goNewUrl(item.jumpType,item.jumpUrl,item.jumpNewsId)"
                    class="img"/>
                <div class="advertisement-text">推广</div>
            </div>
        </div>
    </div>
</template>
<script>
    import API from  './../../assets/js/api'
    export default {
        name:"expressDetails",
        data(){
            return{
                newInfoAdvertisementUrl:API.api.news.newInfoAdvertisement, //首页广告接口
                expressurl:API.api.express.details,//快讯详情页
                marginTop:null,
                datas:null,
                rightAd:[],
                detailsData:{},
                month:null,
                day:null,
                time:null
            }
        },
        methods:{
            getAdData:function (){
                let _this = this
                let params={
                    pageCurrent:1,
                    pageSize:3
                }
                _this.getData(_this.newInfoAdvertisementUrl,params,function (res) {
                    if (res.code === 0) {
                        let data = res.object;
                        let len,arr=[]
                        if(data.length<3){
                            len = 2 - data.length
                            for (var i=0;i<=len;i++){
                                arr.push({
                                    image:null,
                                })
                                _this.rightAd=data.concat(arr)
                            }
                        }else {
                            _this.rightAd=data;
                        }
                    }
                }, (res) => {
                    console.log(res)
                })
            },
            getexpressdetails:function(){
                this.id=this.$route.query.id;
                let _this = this;
                let params = {
                    id:this.id
                };
                _this.postData(_this.expressurl,params,function(res){
                    _this.detailsData = res.object;
                    // console.log(_this.detailsData);
                    _this.month = _this.detailsData.releaseDate.split(' ')[0].split('-')[1];
                    _this.day = _this.detailsData.releaseDate.split(' ')[0].split('-')[2];
                    _this.time = _this.detailsData.releaseDate.split(' ')[1].split(':')[0]+':'+_this.detailsData.releaseDate.split(' ')[1].split(':')[1];
                    _this.week = _this.detailsData.week;
                },(res) => {
                    console.log(res)
                })
            }
        },
        mounted(){
            this.getAdData();
            this.getexpressdetails();
            switch (this.$route.query.type) {
                case 'expressDetails':
                this.parentType = '7×24小时快讯'
                this.$store.commit('SetActiveTab','expressNew')
                break
            }
        }
    }
</script>
<style scoped>
    @import "../news/newsDetails.css";
     .expressDetails{
        padding: 30px 0;
    }
    .clock{

    }
    .month{
        width: 65px;
        height: 65px;
        text-align: center;
        border-radius: 50%;
        background-color: #0a7ff2;
        display: inline-block;

    }
    .day{
        font-size: 32px;
        color: #fff;
        font-weight: 700;
    }
    .day1{
        font-size: 12px;
        color: #8ed0ff;
    }
    .time{
        display: inline-block;
        padding-left: 10px;
    }
    .week{
        font-size: 14px;
        margin: 6px 0 2px;
    }
    .week1{
        font-size: 32px;
    }
    .textdetails{
        padding-left: 82px;
    }
    .title{
        font-size: 26px;
        margin: 20px 0 24px;
    }
    .text1{
        line-height: 28px;
        font-size: 16px;
        margin-bottom: 24px;
        color: #757575;
    }
    .hint{
        font-size: 14px;
        line-height: 22px;
        margin-top: 30px;
        color: #ccc;
        padding-left: 82px;
    }
    .goodbad{
        width: 100%;
        height: 18px;

    }
    .fr{
        float: right;
        font-size: 14px;
        color: #ccc;
        cursor: pointer;
        padding-left: 15px;
    }
    .fr img{
        height: 14px;
    } 
    @media screen and (max-width: 1280px) {
         .textdetails,.hint{
            padding-left: 0;
        }
    }
</style>

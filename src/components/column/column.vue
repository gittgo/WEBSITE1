<template>
<div class="container cl" style="overflow: hidden;margin-top: 21px">
  <div class="content-left">
    <v-banner ref="Banner"
              :columnBanner="columnBanner"
              style="margin-bottom: 30px"></v-banner>
    <div class="content-home cl">
      <v-column-content ref="ColumnContent" ></v-column-content>
    </div>
  </div>
  <div class="content-right">
    <v-right-content ref="RightContent"></v-right-content>
  </div>
</div>
</template>
<script>
import ColumnContent from './../common/contentList'
import RightContent from './../common/rightContent'
import Banner from  './../common/banner'
import API from '../../assets/js/api'
export default {
  name: "column",
  data(){
    return{
      type:'column',  //专栏
      Url: API.api.express.getNewsColumnBanner,
      active:0,
      columnBanner:[],
    }
  },
  components: {
    'v-column-content': ColumnContent,
    'v-right-content': RightContent,
    'v-banner': Banner
  },
  methods:{
    getTabs:function () {
      let _this = this;
      let params={
        pageCurrent:1,
        pageSize:30,
      };
      _this.getData(_this.Url,params,function (res) {
        // console.log(res)
        if (res.code === 0) {
          let data = res.object;
          _this.columnBanner = data;
          _this.$emit('is-footer', true)
        }
      }, (res) => {
        console.log(res)
      })
      setTimeout(function(){
        _this.$emit('is-footer', true)
      },1000);
    }
  },
  mounted(){
    this.$emit('is-footer', false)
    this.getTabs()
  },
}
</script>

<style>
  @import "./../home/home.css";
  @import "./column.css";
</style>

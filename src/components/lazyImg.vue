<template>
  <ul class="img-warp">
    <li v-for="(item,index) in imgList">
        <img :src="item.imgSrc" :class="{'lozy-img':!item.lazy}">
    </li>
  </ul>
</template>

<script>
const srcName = require('../assets/logo.png'); // 这里是为了让JS能打包图片
const imgSrc = require('../assets/loading.gif');
export default {
  name: 'lazyImg',
  data () {
    return {
      imgList:[
          {srcName,imgSrc,lazy:false},
          {srcName,imgSrc,lazy:false},
          {srcName,imgSrc,lazy:false},
          {srcName,imgSrc,lazy:false},
          {srcName,imgSrc,lazy:false},
          {srcName,imgSrc,lazy:false},
      ],
      step:0,
    }
  },
  methods:{
      lazyImg(){ //JS慢慢加载图片
          let img = new Image();
          img.src = this.imgList[this.step].srcName;
          img.onload = this.imgLoaaded();
      },
      imgLoaaded(){ // 加载完成
          this.imgList[this.step].imgSrc = this.imgList[this.step].srcName;
          this.imgList[this.step].lazy = true;
          this.step++;
          setTimeout(()=>{ // 这里延迟2秒是为了看效果
              this.initLazy();
          },1000)
      },
      initLazy(){
          if(this.step>=this.imgList.length){
              return;
          }
          this.lazyImg();
      }
  },
  mounted(){
      this.initLazy();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
    margin:0;
    padding:0;
}
    .img-warp{
        width:100%;
        display:flex;
        justify-content: space-around;
        flex-wrap: wrap;
    }
    .img-warp li{
        width:45vw;
        height:45vw;
        line-height: 45vw;
        border:1px solid #cccccc;
    }
    .img-warp img{
        width: 170px;
    }
    .img-warp .lozy-img{
        width:45px;
        height:45px;
    }
</style>

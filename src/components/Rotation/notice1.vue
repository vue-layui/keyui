<template>
  <div>
    <div id="box">
      <ul id="con1" ref="con1" :class="{anim:animate==true}">
        <li v-for='item in items'>{{item.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
    export default {
        name: "notice1",
      data() {
        return {
          animate:false,
          items:[  //消息列表对应的数组
            {name:"财经新闻1"},
            {name:"财经新闻2"},
            {name:"财经新闻3"}
          ]
        }
      },
      created(){
        setInterval(this.scroll,1500) // 在钩子函数中调用我在method 里面写的scroll()方法，注意此处不要忘记加this,我在这个位置掉了好几次坑，都是因为忘记写this。
      },
      methods: {
        scroll(){
          let con1 = this.$refs.con1;
          con1.style.marginTop='-30px';
          this.animate=!this.animate;
          var that = this; // 在异步函数中会出现this的偏移问题，此处一定要先保存好this的指向
          setTimeout(function(){
            that.items.push(that.items[0]);
            that.items.shift();
            con1.style.marginTop='0px';
            that.animate=!that.animate;  // 这个地方如果不把animate 取反会出现消息回滚的现象，此时把ul 元素的过渡属性取消掉就可以完美实现无缝滚动的效果了
          },500)
        }
      },
    }
</script>

<style scoped>
  *{
    margin: 0 ;
    padding: 0;
  }
  #box{
    width: 300px;
    height: 32px;
    line-height: 30px;
    overflow: hidden;
    padding-left: 30px;
    border: 2px solid darkseagreen;
    transition: all 0.5s;
    border-radius: 7px;
  }
  .anim{
    transition: all 0.5s;
  }
  #con1 li{
    list-style: none;
    line-height: 30px;
    height: 30px;
    font-weight: bold;
  }
</style>

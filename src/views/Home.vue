<template>
  <div>
    <ul>
      <li v-for="(item,index) in pics" :key="index">
        <img
          :src="item"
          alt
          @mouseenter="showPicMsg(index)"
          @mouseout="hidePicMsg()"
          @click="gotoDetail(index)"
        />
        <span
          v-if="currentindex==index&&currentindex>-1"
          class="showPX"
        >{{picsInfo[index].width}}✖{{picsInfo[index].height}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  //比较简单,请别见笑。
  data() {
    return {
      currentindex: -1,
      pics: [
        "https://t7.baidu.com/it/u=378254553,3884800361&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597047628&t=ed92ee981e56cfb90c27bbdfb470f8a5",
        "https://t8.baidu.com/it/u=3571592872,3353494284&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597047628&t=fa08de43f5e63a01c3ca1174a41fd138",
        "https://t7.baidu.com/it/u=3616242789,1098670747&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597047628&t=df626c9b5cfa9c7ea8ef9d89a3c7a0b2",
        "https://t8.baidu.com/it/u=1484500186,1503043093&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597047628&t=3606a8b89d25f7fd8e4c05565e2f02a1",
        "https://t8.baidu.com/it/u=2247852322,986532796&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597047628&t=c43ee834b29068077aa94949590d5998",
        "https://t9.baidu.com/it/u=1761131378,1355750940&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597062700&t=acb179176b24ef8c5464546745dc0748",
        "https://t9.baidu.com/it/u=86853839,3576305254&fm=79&app=86&size=h300&n=0&g=4n&f=jpeg?sec=1597062700&t=023fa31e6cadc9f512579c73a021ac1c",
      ],
      picsInfo: [],
    };
  },

  methods: {
    // 获取图片像素
    getImgInfo() {
      let imgInfo = {};
      for (let i = 0; i < this.pics.length; i++) {
        let img = new Image();
        img.src = this.pics[i];
        img.onload = function () {
          imgInfo.width = img.width;
          imgInfo.height = img.height;
          return imgInfo;
        };
        this.picsInfo.push(imgInfo);
      }
    },
    // 鼠标移入
    showPicMsg(index) {
      this.currentindex = index;
      console.log("鼠标意移入");
    },
    //鼠标移出
    hidePicMsg() {
      this.currentindex = -1;
    },
    // 带参数跳转到详情页面
    gotoDetail(index) {
      this.$router.push({
        path: "ImgDetail",
        query: { id: index, nextImg: this.pics },
      });
    },
  },
  mounted() {
    this.getImgInfo();
  },
};
</script>

<style scoped lang="less">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
}
a {
  color: #42b983;
}
li {
  position: relative;
  .showPX {
    position: absolute;
    left: 30px;
    bottom: 30px;
    opacity: 0.8;
    background-color: whitesmoke;
    color: black;
  }
}
</style>

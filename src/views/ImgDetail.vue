<template>
  <div>
    <button @click="goprev()" class="btnPrev">上一张</button>
    <img :src="nextImg[currentImg]" alt />
    <button @click="gonext()" class="btnNext">下一张</button>
  </div>
</template>

<script>
export default {
  name: "ImgDetail",
  data() {
    return {
      nextImg: [],
      currentImg: Number,
    };
  },
  methods: {
    goprev() {
      if (this.currentImg >= 1) {
        this.currentImg--;
      } else if (this.currentImg == 0) {
        alert("已经是第一张了");
      }
    },
    gonext() {
      if (this.currentImg < this.nextImg.length - 1) {
        this.currentImg++;
      } else if (this.currentImg == this.nextImg.length - 1) {
        alert("已经是最后一张了");
      }
    },
  },
  mounted() {
    console.log(this.$route.query.id);
    this.nextImg = this.$route.query.nextImg;
    this.currentImg = this.$route.query.id;
  },
};
</script>

<style>
</style>
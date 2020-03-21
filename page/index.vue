<template>
  <div class="apple-page">
    <ul>
      <li @click="LeftMove"><</li>
      <li :class="{'action':index==1}" @click="cutPage(1)">1</li>
      <li v-if="showLeft">...</li>
      <li
        :class="{'action':index==(p + (s + 1))}"
        :id="p + (s + 1)"
        @click="cutPage(p+s+1)"
        v-for="p in 5"
        :key="p+s+1"
      >{{p + s + 1}}</li>
      <li v-if="showRight">...</li>
      <li :class="{'action':index==sumPage}" @click="cutPage(10)">{{sumPage}}</li>
      <li @click="rightMove">></li>
    </ul>
    <div class="show-text">
      当前{{index}}页
      共{{sumPage}}页
    </div>
  </div>
</template>

<script>
export default {
  name: "ApplePage",
  props: {
    sumPage: {
      // 总共页数
      type: Number,
      default: () => 10
    }
  },
  data() {
    return {
      index: 1, // 分页选中
      showLeft: false, // 显示左边...
      showRight: true, // 显示右边...
      s: 0 // 开始叠加
    };
  },
  watch: {
    index() {
      if (this.index > 4) {
        this.showLeft = true;
      }
      if (this.index >= this.sumPage - 3) {
        this.showRight = false;
      }
      if (this.index <= 4) {
        this.s = 0
        this.showLeft = false;
      }
      if (this.index < this.sumPage - 3) {
        this.showRight = true;
      }
      this.$emit("cut-page", this.index)
    }
  },
  methods: {
    cutPage(index) {
      //改变页
      if (index == this.sumPage) {
        this.s = index - 7;
      }
      if(index == this.sumPage - 2) {
        this.s = index - 5
      }
      if (index >= 4 && index <= this.sumPage - 3 && index != this.sumPage) {
        this.s = index - 4;
      }
      this.index = index;
    },
    LeftMove() {
      // 往左移动
      if (this.index > 4 && this.index < this.sumPage - 3)
        this.s = this.index - 5;
      if (this.index > 1) this.index--;
    },
    rightMove() {
      // 往右移动
      if (this.index >= 4 && this.index < this.sumPage - 3) {
        this.s = this.index - 3;
      }
      if (this.index < this.sumPage) this.index++;
    }
  }
};
</script>

<style lang="scss" scoped>
.apple-page {
  display: flex;
  .show-text {
    line-height: 30px;
  }
  ul {
    margin: 0px;
    list-style: none;
    overflow: hidden;
    li {
      width: 30px;
      height: 30px;
      line-height: 30px;
      background: paleturquoise;
      float: left;
      color: white;
      margin-right: 10px;
      cursor: pointer;
    }
    li.action {
      background: blue;
    }
    li:hover {
      color: black;
    }
  }
}
</style>
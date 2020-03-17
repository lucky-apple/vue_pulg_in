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
        this.showLeft = false;
      }
    }
  },
  methods: {
    cutPage(index) {
      //改变页
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
  ul {
    list-style: none;
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
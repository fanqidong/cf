<template>
  <div class="select-wrapper" @click="toggleSelect($event)">
    <div class="select-show">
      <span class="select-value">{{curValue}}</span>
      <span class="select-arrow"></span>
    </div>
    <ul class="select-list" v-show="isShow">
      <li
        v-for="(item,index) in selectOptions"
        :key="index"
        @click.stop="chooseOption(index)"
      >{{item.text}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    selectOptions: {
      type: Array,
      default: []
    }
  },
  data() {
    return {
      curValue: this.selectOptions[0].text || "",
      isShow: false
    };
  },
  methods: {
    chooseOption(index) {
      this.isShow = false;
      this.curValue = this.selectOptions[index].text;
      this.$emit("choose-select", this.selectOptions[index]);
    },
    toggleSelect($event) {
      this.isShow = !this.isShow;
      document.documentElement.onclick = e => {
        let ev = e || event;
        ev.currentTarget !== $event.currentTarget && (this.isShow = false);
      };
    }
  },
  mounted(){
  }
};
</script>

<style lang="scss" scoped>
.select {
  &-wrapper {
    position: relative;
    text-align: center;
    width: 60px;
  }
  &-show {
    position: relative;
    width: 100%;
    border: 1px solid #e3e3e3;
    cursor: pointer;
    height: 25px;
    line-height: 25px;
    border-radius: 3px;
    background: #fff;
  }
  &-list {
    position: absolute;
    left: 0;
    top: 25px;
    width: 100%;
    background: #fff;
    border: 1px solid #e3e3e3;
    z-index: 5;
    li {
      padding: 0 8px;
      line-height: 25px;
      background: #fff;
      cursor: pointer;
      &:hover {
        background: #e3e3e3;
      }
    }
  }
}
</style>


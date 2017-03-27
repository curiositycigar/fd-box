<template>
  <div class="f-box" :style="getContentStyle">
    <div v-show="header" class="f-box-header">
      <i :class="headerIconClass"></i>
      <span>{{ title }}</span>
    </div>
    <div class="f-box-body" :style="getBodyHeight">
      <div class="f-box-bar" v-for="item in barArray" :style="getStyle(item)">
        <slot :name="item.index"></slot>
      </div>
    </div>
  </div>
</template>

<script type="text/babel">
  // width,height,icon格式,是否显示Header,分栏条数
  export default {
    data() {
      return {
        barArray: ['100%'],
        headerHeight: {
          tiny: 32,
          small: 34,
          big: 40,
          large: 50
        }
      };
    },
    created() {
      let reBars = [];
      if (typeof this.bars === 'number') {
        let bar = 100 / this.bars;
        for (let i = 0; i < this.bars; i++) {
          reBars.push({
            index: i + 1,
            width: bar + '%'
          });
        }
      } else if (typeof this.bars === 'object' && this.bars.length) {
        let count = 0;
        for (let i = 0; i < this.bars.length; i++) {
          count += this.bars[i];
        }
        let minBar = 100 / count;
        reBars = this.bars.map(function (value, index) {
          return {
            index: index,
            width: minBar * value + '%'
          };
        });
      }
      this.barArray = reBars;
    },
    methods: {
      getStyle(item) {
        return 'width:' + item.width;
      }
    },
    computed: {
      getBodyHeight() {
        let height = this.header ? Number.parseInt(this.height) - this.headerHeight[this.size] : Number.parseInt(this.height);
        return 'height:' + height + 'px';
      },
      getContentStyle() {
        return 'width:' + this.width + '; height:' + this.height;
      },
      headerIconClass() {
        return 'icon-' + this.type + ' ' + this.size;
      }
    },
    props: {
      title: {
        type: String,
        default: ''
      },
      height: {
        type: String,
        default: '300px'
      },
      width: {
        type: String,
        default: '100%'
      },
      type: {
        type: String,
        default: 'warning'
      },
      header: {
        type: Boolean,
        default: true
      },
      bars: {
        type: [Number, Array],
        default: 1
      },
      size: {
        type: String,
        default: 'small'
      }
    }
    //  ['title', 'height', 'width', 'type', 'header', 'bars']
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "css/font-style.css"
  .f-box
    border: solid 1px #d1dbe5;
    border-radius: 5px;
    .f-box-header
      box-sizing: border-box
      width: 100%
      line-height: 100%
      padding: 10px 0 10px 15px
      border-bottom: solid 1px #d1dbe5
      i
        display: inline-block
        vertical-align: top
        &.tiny
          width: 12px
          height: 12px
          font-size: 12px
          + span
            line-height: 12px
            font-size: 12px
        &.small
          width: 14px
          height: 14px
          font-size: 14px
          + span
            line-height: 14px
            font-size: 14px
        &.big
          width: 20px
          height: 20px
          font-size: 20px
          + span
            line-height: 20px
            font-size: 16px
        &.large
          width: 30px
          height: 30px
          font-size: 30px
          + span
            line-height: 30px
            font-size: 20px
      span
        display: inline-block
        height: 100%
        margin: auto 10px
        font-weight: 600
        vertical-align: top
    .f-box-body
      display: inline-block
      width: 100%
      .f-box-bar
        padding: 10px
        box-sizing: border-box
        float: left
        height: 100%
      > .f-box-bar + .f-box-bar
        border-left: solid 1px #d1dbe5
</style>

<template>
  <div class="range-slider">
    <div class="lines-container">
      <div class="empty-space">

      </div>
      <div
          class="line"
          v-for="(line, index) in lines"
          :key="index"
          :class="line.class"
      >
        <span class="line-value">
          {{line.value}}
        </span>
      </div>
      <div class="empty-space">

      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    /**
     * @property {number} min
     */
    min: {
      type: Number,
      default: 1
    },
    /**
     * @property {number} max
     */
    max: {
      type: Number,
      default: 10
    },
    /**
     * @property {number} step
     */
    step: {
      type: Number,
      default: 1
    }
  },
  data() {
    return {
      lines: []
    };
  },
  mounted() {
    this.generateLines();
  },
  methods: {
    generateLines() {
      let i = this.min;
      while (i <= this.max) {
        const elem = {
          value: +i.toFixed(2),
          class: i % 1 === 0 ? 'big' : 'small'
        };
        this.lines.push(elem);
        i = +i.toFixed(2) + this.step;
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .range-slider{
    .lines-container{
      display: flex;
      align-items: flex-end;
      padding: 8px 0 25px;
      overflow: auto;
      height: 61px;
    }
    .empty-space{
      min-width: 50%;
      flex: 1 0 50%;
      height: 1px;
      &:last-child{
        min-width: calc(50% - 3px);
        flex: 1 0 calc(50% - 3px);
      }
    }
    .line{
      width: 1px;
      margin-right: 10px;
      background: #2de811;
      border-radius: 2px;
      min-width: 1px;
      position: relative;
      &.big{
        height: 17px;
      }
      &.small{
        height: 12px;
      }
      &.active{
        background: #fe7f01;
        .value{
          color: #fe7f01;
        }
      }
      &-value{
        font-style: normal;
        font-weight: 500;
        font-size: 8px;
        color: #49de0c;
        position: absolute;
        bottom: -10px;
        transform: translateX(-50%);
      }
    }
  }
</style>
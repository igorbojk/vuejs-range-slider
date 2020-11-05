<template>
  <div class="range-slider">
    <div class="lines-container">
      <div class="empty-space">

      </div>
      <div
          class="line"
          v-for="(line, index) in lines"
          :key="index"
          :class="generateLineClass(line)"
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
    },

    /**
     * @property {number} startValue
     */
    startValue: {
      type: Number,
      default: 5
    },

    /**
     * @property {number} startValue
     */
    startNextValue: {
      type: Number,
      default: 6
    }
  },
  data() {
    return {
      lines: [],
      currentValue: 5,
      nextValue: 6
    };
  },
  mounted() {
    this.currentValue = this.startValue;
    this.nextValue = this.startNextValue;
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
    },
    /**
     * @param line {{class: String, value: Number}}
     */
    generateLineClass(line) {
      let classes = line.class;
      const nextValue = +this.nextValue.toFixed(1);
      if (line.value === nextValue) {
        classes += ' next';
      }

      if (this.currentValue < nextValue) {
        if (line.value >= this.currentValue && line.value <= nextValue) {
          classes += " active";
        }
      } else {
        if (line.value <= this.currentValue && line.value >= nextValue) {
          classes += " active";
        }
      }

      return classes;
    }
  }
}
</script>

<style scoped lang="scss">
  .range-slider{
    ::-webkit-scrollbar{
      height: 0;
    }
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
      margin-right: 18px;
      background: #b4bfb1;
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
        .line-value{
          color: #fe7f01;
        }
      }
      &-value{
        font-style: normal;
        font-weight: 500;
        font-size: 10px;
        color: #b4bfb1;
        position: absolute;
        bottom: -14px;
        transform: translateX(-50%);
      }
    }
  }
</style>
<template>
  <div
    slot="reference"
    class="flight"
    :style="{
      'background-color': statusColor,
      'margin-top': 0.1 * cellHeight + 'px'
    }"
    @click="onClick"
    @dragstart="handleStart"
    @drag="handleDrag"
    @dragend="handleEnd"
    draggable="true"
  >
    <div class="content">
      <span>{{ item.filghtNumber }}</span>
      <span>{{ item.startAirport }}</span>
      <span>{{ item.endAirport }}</span>
    </div>
  </div>
</template>

<script>
const NOW_PLAN = "#D5F8EA";
const FUTHER_PLAN = "#BFF2FE";
const PAST_PLAN = "#F2F2F2";
export default {
  name: "GanttMain",
  props: {
    data: Object,
    item: Object,
    updateTimeLines: Function,
    cellHeight: Number,
    startTimeOfRenderArea: Number
  },
  computed: {
    statusColor() {
      return FUTHER_PLAN; // Future
    }
  },
  created () {
    console.log('data:', this.data)
    console.log('item:', this.item)
  },
  methods: {
    onClick () {
      this.updateTimeLines(this.item.start, this.item.end);
    },
    handleStart (e) {
      console.log('dragstart-在元素开始被拖动时候触发')
    },
    handleDrag () {
      console.log('drag-在元素被拖动时候反复触发')
    },
    handleEnd () {
      console.log('dragend-在拖动操作完成时触发')
    }
  }
};
</script>

<style lang="scss" scoped>
.flight {
  display: flex;
  align-items: center;
  box-sizing: border-box;
  height: 80%;
  border: 1px solid #f0f0f0;
  border-radius: 5px;
  color: #333333;
  padding-left: 5px;
  font-size: 0.8rem;
  border: 1px solid #f0f0f0;
  // opacity: 0.8;
}
</style>

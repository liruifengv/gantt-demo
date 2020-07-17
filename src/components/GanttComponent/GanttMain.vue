<template>
  <el-popover placement="bottom" trigger="hover">
    <div
      slot="reference"
      class="plan"
      :style="{
        'background-color': statusColor,
        'margin-top': 0.1 * cellHeight + 'px'
      }"
      @click="onClick"
    >
      <div class="runTime">
        <span>{{ item.filghtNumber }}</span>
        <span>{{ item.startAirport }}</span>
        <span>{{ item.endAirport }}</span>
      </div>
    </div>

    <div class="detail">
      <ul>
        <li>
          <span>航班号：</span><span>{{ item.filghtNumber }}</span>
        </li>
        <li>
          <span>起飞机场：</span><span>{{ item.startAirport }}</span>
        </li>
        <li>
          <span>降落机场：</span><span>{{ item.endAirport }}</span>
        </li>
      </ul>
    </div>
  </el-popover>
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
    console.log('■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■')
    console.log('data:', this.data)
    console.log('item:', this.item)
    console.log('■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■')
  },
  methods: {
    onClick() {
      this.updateTimeLines(this.item.start, this.item.end);
    }
  }
};
</script>

<style lang="scss" scoped>
.middle {
  flex: 1;
  text-align: center;
  padding-left: 5px;
}
.runTime {
}
.plan {
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

.detail {
  .header {
    text-align: center;
    font-size: 1rem;
  }
}

.detail ul {
  list-style: none;
  padding: 0px;
  li {
    span {
      display: inline-block;
      width: 80px;
      color: #777;
      font-size: 0.8rem;
    }
    span:first-child {
      text-align: right;
    }

    span:last-child {
    }
  }
}
</style>

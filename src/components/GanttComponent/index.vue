<template>
    <div class="container">
      <Gantt
        :currentTime="currentTime"
        :startTime="startTime"
        :endTime="endTime"
        :cellWidth="cellWidth"
        :cellHeight="cellHeight"
        :timeLines="timeLines"
        :titleHeight="titleHeight"
        :scale="scale"
        :titleWidth="titleWidth"
        showCurrentTime
        :hideHeader="hideHeader"
        :dataKey="dataKey"
        :arrayKeys="arrayKeys"
        :scrollToPostion="positionA"
        @scrollLeft="scrollLeftA"
        :datas="ganttData"
      >
        <template v-slot:block="{ data, item }">
          <GanttMain
            :data="data"
            :updateTimeLines="updateTimeLines"
            :cellHeight="cellHeight"
            :item="item"
          ></GanttMain>
        </template>
        <template v-slot:left="{ data }">
          <GanttLeft :data="data"></GanttLeft>
        </template>
      </Gantt>
    </div>
</template>

<script>

import GanttLeft from "./GanttLeft.vue";
import GanttMain from "./GanttMain.vue";
import { mockDatas } from "../../mock/index.js";
import dayjs from "dayjs";

export default {
  name: "GanttComponent",
  components: { GanttLeft, GanttMain },
  data() {
    return {
      timeLines: [],
      cellWidth: 40,
      cellHeight: 40,
      titleHeight: 80,
      titleWidth: 150,
      scale: 60,
      scrollToTime: dayjs()
        .add(1, "day")
        .toString(),
      scrollToPostion: { x: 10000, y: 10000 },
      hideHeader: false,
      hideSecondGantt: false,
      scrollToY: 0,
      positionB: {},
      positionA: {}
    };
  },
  watch: {
    scrollToY(val) {
      this.positionA = { x: val };
    }
  },
  props: {
    ganttData: {
      type: Array
    },
    arrayKeys: {
      type: Array
    },
    currentTime: '',
    startTime: '',
    endTime: '',
    dataKey: {
      type: String,
      default: 'id'
    }
  },
  mounted() {
  },
  methods: {
    blockDrop (e) {
      console.log('■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■')
      console.log('blockDrop:', e)
      console.log('■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■')
    },
    updateTimeLines(timeA, timeB) {
      this.timeLines = [
        {
          time: timeA
        },
        {
          time: timeB,
          color: "#747e80"
        }
      ];
    },
    scrollLeftA(val) {
      this.positionB = { x: val };
    },
    scrollLeftB(val) {
      this.positionA = { x: val };
    }
  }
};
</script>

<style scoped>
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  flex: 1;
}

>>> .el-slider {
  width: 100px;
}
</style>

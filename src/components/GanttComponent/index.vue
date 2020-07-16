<template>
  <div id="app">
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
        <template v-slot:title>铁胆火车侠日程表 </template>
      </Gantt>
    </div>
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
      cellWidth: 50,
      cellHeight: 30,
      titleHeight: 40,
      titleWidth: 250,
      scale: 60,
      scrollToTime: dayjs()
        .add(1, "day")
        .toString(),
      scrollToPostion: { x: 10000, y: 10000 },
      hideHeader: false,
      hideSecondGantt: false,
      arrayKeys: ["gtArray", "error"],
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
body {
  font: 12px;
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

#app {
  display: flex;
  flex-direction: column;
  padding: 0 10px;
  height: calc(100vh - 2px);
}

label {
  margin-left: 10px;
}
input {
  width: 40px;
  height: 20px;
  vertical-align: middle;
}
input[type="range"] {
  width: 100px;
}
.top-bar {
  height: 40px;
}

.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.main-footer {
  /* height: 30px; */
}

>>> .el-slider {
  width: 100px;
}
</style>

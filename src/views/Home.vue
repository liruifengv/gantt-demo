<template>
  <div class="home">
    <GanttComponent 
    :ganttData="ganttData" 
    :currentTime="currentTime"
    :startTime="startTime"
    :endTime="endTime"
    :dataKey="dataKey"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import GanttComponent from '@/components/GanttComponent'
import { mockDatas } from "../mock/index.js"
import dayjs from "dayjs";

export default {
  name: 'Home',
  data() {
    return {
      ganttData: [],
      times: [
        dayjs()
          .subtract(5, "hour")
          .toString(),
        dayjs()
          .add(2, "day")
          .add(2, "hour")
          .toString()
      ],
      currentTime: '',
      startTime: '',
      endTime: '',
      dataKey: 'id'
    }
  },
  components: {
    GanttComponent
  },
  mounted() {
    this.getData()
    this.getCurrentTime()
  },
  methods: {
    getData() {
      this.ganttData = mockDatas(5, 5, this.times);
    },
    getCurrentTime () {
      const timeNow = setInterval(() => {
        this.currentTime = dayjs().toString();
      }, 1000);
      this.$once("hook:beforeDestroy", () => {
        clearInterval(timeNow);
      });
      // this.startTime = dayjs().subtract(2, "hour").toString()
      this.startTime = dayjs().subtract(2, "day").toString()
      this.endTime = dayjs().add(2, "day").toString()
    }
  }
}
</script>

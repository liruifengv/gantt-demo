<template>
  <div class="home">
    <GanttComponent 
    :ganttData="ganttData" 
    :currentTime="currentTime"
    :startTime="startTime"
    :endTime="endTime"
    :dataKey="dataKey"
    :arrayKeys="arrayKeys"
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
      dataKey: 'childId',
      arrayKeys: ['childArrary']
    }
  },
  components: {
    GanttComponent
  },
  created() {
    this.getData()
    this.getCurrentTime()
  },
  methods: {
    getData() {

      this.ganttData = [
        {
          id: 1,
          currentAirort: '北京机场',
          number: 'B-1323',
          model: 'H125',
          childArrary: [
            {
              childId: 1,
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/16 22:00:00',
              end: '2020/07/16 23:00:00',
            },
            {
              childId: 2,
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/17 08:00:00',
              end: '2020/07/17 10:00:00',
            }
          ]
        },
        {
          id: 1,
          currentAirort: '北京机场',
          number: 'B-1323',
          model: 'H125',
          childArrary: [
            {
              childId: 1,
              filghtNumber: '4343',
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/16 22:00:00',
              end: '2020/07/16 23:00:00',
            },
            {
              childId: 2,
              filghtNumber: '4343',
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/17 08:00:00',
              end: '2020/07/17 10:00:00',
            }
          ]
        },
        {
          id: 2,
          currentAirort: '北京机场',
          number: 'B-1323',
          model: 'H125',
          childArrary: [
            {
              childId: 1,
              filghtNumber: '4343',
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/16 22:00:00',
              end: '2020/07/16 23:00:00',
            },
            {
              childId: 2,
              filghtNumber: '4343',
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/17 08:00:00',
              end: '2020/07/17 10:00:00',
            }
          ]
        },
        {
          id: 3,
          currentAirort: '北京机场',
          number: 'B-1323',
          model: 'H125',
          childArrary: [
            {
              childId: 1,
              filghtNumber: '4343',
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/16 22:00:00',
              end: '2020/07/16 23:00:00',
            },
            {
              childId: 2,
              filghtNumber: '121',
              startAirport: '天津机场',
              endAirport: '北京机场',
              start: '2020/07/17 08:00:00',
              end: '2020/07/17 10:00:00',
            }
          ]
        }
      ]
      // this.ganttData = mockDatas(5, 5, this.times);
      console.log('■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■')
      console.log('ganttData:', this.ganttData)
      console.log('■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■■')
    },
    getCurrentTime () {
      this.currentTime = dayjs().toString();

      const timeNow = setInterval(() => {
        this.currentTime = dayjs().toString();
      }, 1000);
      this.$once("hook:beforeDestroy", () => {
        clearInterval(timeNow);
      });
      this.startTime = dayjs().subtract(3, "hour").toString()
      this.endTime = dayjs().add(2, "day").toString()
    }
  }
}
</script>

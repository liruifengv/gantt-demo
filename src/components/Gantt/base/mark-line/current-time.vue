<template>
  <mark-line
    :markLineTime="currentTime"
    :getPositonOffset="getPositonOffset"
    color="rgba(255,0,0,.4)"
  ></mark-line>
</template>

<script>
import dayjs from "dayjs";
import MarkLine from "./index.vue";
export default {
  name: "CurrentTime",
  components: { MarkLine },
  props: {
    getPositonOffset: {
      type: Function,
      required: true
    },
    currentTime: ''
  },
  data() {
    return {
    };
  },
  created() {
  }
};
</script>

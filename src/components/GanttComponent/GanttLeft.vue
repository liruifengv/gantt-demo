<template>
  <div class="left-item" :class="[
    unassigned
  ]">
    <div class="colorBar" />
    <div class='content'>
      <div class="content-item model" :title="data.model">{{ data.model }}</div>
      <div class="content-item number" :title="data.number">{{ data.number }}</div>
      <div class="content-item currentAirort" :title="data.currentAirort">{{ data.currentAirort }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "GanttMain",
  props: {
    data: Object
  },
  computed: {
    unassigned () {
      return this.data.unassigned ? `left-item--unassigned` : ''
    }
  }
};
</script>

<style scoped lang="scss">
.left-item {
  display: flex;
  box-sizing: border-box;
  overflow: hidden;
  height: 100%;
  width: 100%;
  padding: 0 5px 0 0;
  border-radius: 8px 0 0 8px;
  align-items: center;
  background:rgba(180,209,125,0.2);
}
.colorBar {
  width:10px;
  height:40px;
  background:rgba(180,209,125,1);
  border-radius:7px 0px 0px 7px;
}
.left-item--unassigned {
  background:rgba(241,206,99,.2);
  .colorBar {
    background:rgba(255,205,49,1);
  }
}

.content {
  display: flex;
  overflow: hidden;
}
.content-item {
  width: 33.3%;
  overflow: hidden;
  margin-left: 5px;
  white-space:nowrap;
  cursor: pointer;
}
</style>

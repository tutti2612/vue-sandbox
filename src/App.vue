<template>
  <div id="app">
    <status-select :options="options" placeholder="ステータスで絞り込む" />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import StatusSelect from "./components/StatusSelct.vue";

export default Vue.extend({
  name: "App",
  components: {
    StatusSelect
  },
  data() {
    return {
      options: [
        {
          label: "ログイン済",
          value: "1",
          isSelected: false
        },
        {
          label: "未ログイン",
          value: "2",
          isSelected: false
        },
        {
          label: "ロック中",
          value: "3",
          isSelected: false
        }
      ]
    };
  }
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

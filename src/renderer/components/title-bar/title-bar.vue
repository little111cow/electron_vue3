<template>
  <div class="window-title" v-if="!IsUseSysTitle && isNotMac && !IsWeb">
    <!-- 软件logo预留位置 -->
    <div style="-webkit-app-region: drag" class="logo">
      <img src="@renderer/assets/icons/favicon.ico" class="icon-logo" />
    </div>
    <!-- 菜单栏 -->
    <div class="menu">
      <div v-for="item in ['文件', '编辑', '选择', '运行']" class="menu_item">
        {{ item }}
      </div>
    </div>
    <!-- 中间标题位置 -->
    <div style="-webkit-app-region: drag" class="title">littlecow</div>
  </div>
  <div v-else-if="!IsUseSysTitle && !isNotMac" class="window-title"></div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const { ipcRendererChannel, systemInfo } = window;

const IsUseSysTitle = ref(false);
const mix = ref(false);
const isNotMac = ref(false);
const IsWeb = ref(Boolean(__ISWEB__));

isNotMac.value = systemInfo.platform !== "darwin";

ipcRendererChannel.IsUseSysTitle.invoke().then((res) => {
  IsUseSysTitle.value = res;
});
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.window-title {
  width: 100%;
  height: 30.5px;
  line-height: 30px;
  background-color: #fff;
  display: flex;
  -webkit-app-region: drag;
  // position: fixed;
  top: 0;
  z-index: 99999;
  user-select: none;

  .icon-logo {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }

  .title {
    width: 80%;
    text-align: center;
    color: #9d9d9d;
  }

  .menu {
    height: 100%;
    width: 20%;
    display: flex;
    -webkit-app-region: no-drag; // 不加会导致鼠标事件不可用

    .menu_item {
      margin-left: 2%;
      cursor: pointer;

      &:hover {
        background-color: rgba(57, 57, 57, 0.2);
      }
    }
  }

  .logo {
    margin: 0 10px;
  }

  .controls-container {
    display: flex;
    flex-grow: 0;
    flex-shrink: 0;
    text-align: center;
    position: fixed;
    z-index: 3000;
    -webkit-app-region: no-drag;
    height: 100%;
    width: 138px;
    margin-left: auto;

    .windows-icon-bg {
      display: inline-block;
      -webkit-app-region: no-drag;
      height: 100%;
      width: 33.34%;
      color: rgba(129, 129, 129, 0.6);

      .icon-size {
        width: 12px;
        height: 15px;
        vertical-align: -0.15em;
        fill: currentColor;
        overflow: hidden;
      }
    }

    .windows-icon-bg:hover {
      background-color: rgba(182, 182, 182, 0.2);
      color: #333;
      cursor: pointer;
    }

    .close-icon:hover {
      background-color: rgba(232, 17, 35, 0.9);
      color: #fff;
      cursor: pointer;
    }
  }
}
</style>

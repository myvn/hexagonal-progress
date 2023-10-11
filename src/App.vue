<template>
  <div id="app">
    <h1>HexagonalProgress使用文档</h1>
    <div style="margin-top: 40px;display: flex;justify-content: flex-start;align-items: flex-start;">
      <div style="display: flex;flex-direction: column;justify-content: flex-start;align-items: flex-start;">
        <h2>参数描述</h2>

        <div :key="descKey"
             style="width: 400px;"
             v-for="(descValue,descKey) in optionDes">
          <p style="text-align: left;text-indent: 2em;">{{ descKey }}:{{ descValue }}</p>
        </div>
      </div>
      <div style="width: 1px;height: 500px;background: #2c3e50;margin-right: 40px;"></div>

      <div style="display: flex;flex-direction: column;justify-content: flex-start;align-items: flex-start;">
        <h2>option 实例</h2>

        <div style="margin-left: 80px;width: 400px;text-align: left;">
          {
          <p style="text-align: left;text-indent: 2em;"> borderColor: '#8ee6ff', </p>
          <p style="text-align: left;text-indent: 2em;"> progressColor: '#0dc1f2',</p>
          <p style="text-align: left;text-indent: 2em;"> bgColor: 'rgba(24,160,206,0.12)',</p>
          <p style="text-align: left;text-indent: 2em;">fontColor: '#0dc1f2',</p>
          <p style="text-align: left;text-indent: 2em;">fontSize: '16px',</p>
          <p style="text-align: left;text-indent: 2em;">width: '100px',</p>
          <p style="text-align: left;text-indent: 2em;">startRad: -120,</p>
          <p style="text-align: left;text-indent: 2em;">number: 0.11,</p>
          }
        </div>
      </div>
      <div style="width: 1px;height: 500px;background: #2c3e50;margin-right: 40px;"></div>

      <div style="display: flex;flex-direction: column;justify-content: flex-start;align-items: flex-start;">
        <h2> 实例</h2>
        <div style="display: flex;justify-content: flex-start;align-items: center;">
          <HexagonalProgress :key="index" v-for="(item,index) in list" :option="item"></HexagonalProgress>
        </div>
        <div style="display: flex;justify-content: flex-start;align-items: center;">
          <HexagonalProgress :key="index" v-for="(item,index) in list1" :option="item"></HexagonalProgress>
        </div>

      </div>

    </div>


  </div>
</template>

<script>
import HexagonalProgress from "@/components/HexagonalProgress.vue";

export default {
  name: 'App',
  components: {
    HexagonalProgress
  },
  data() {
    return {
      optionDes: {
        borderColor: '边框颜色  String',
        progressColor: '进度颜色 String',
        bgColor: '背景色 String',
        fontColor: '字体颜色 String',
        fontSize: '字体大小（单位px） String',
        width: '宽度（单位px）String',
        startRad: '初始角度（-360°,360°） Number',
        number: "进度（0-1）Number",
      },
      list: [
        {
          // 边框颜色
          borderColor: '#8ee6ff',
          // 进度颜色
          progressColor: '#0dc1f2',
          // 背景色
          bgColor: 'rgba(24,160,206,0.12)',
          // 字体颜色
          fontColor: '#0dc1f2',
          // 字体大小
          fontSize: '10px',
          // 宽度：180px
          width: '100px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 0.11,
        },
        { // 边框颜色
          borderColor: '#8ee6ff',
          // 进度颜色
          progressColor: '#0dc1f2',
          // 背景色
          bgColor: 'rgba(24,160,206,0.12)',
          // 字体颜色
          fontColor: '#0dc1f2',
          // 字体大小
          fontSize: '15px',
          // 宽度：180px
          width: '150px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 0.2144,
        },
        { // 边框颜色
          borderColor: '#8ee6ff',
          // 进度颜色
          progressColor: '#0dc1f2',
          // 背景色
          bgColor: 'rgba(24,160,206,0.12)',
          // 字体颜色
          fontColor: '#0dc1f2',
          // 字体大小
          fontSize: '18px',
          // 宽度：180px
          width: '180px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 0.5,
        },
        { // 边框颜色
          borderColor: '#8ee6ff',
          // 进度颜色
          progressColor: '#0dc1f2',
          // 背景色
          bgColor: 'rgba(24,160,206,0.12)',
          // 字体颜色
          fontColor: '#0dc1f2',
          // 字体大小
          fontSize: '20px',
          // 宽度：180px
          width: '200px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 1,
        },


      ],
      list1: [
        { // 边框颜色
          borderColor: '#FFAC9A',
          // 进度颜色
          progressColor: '#e55112',
          // 背景色
          bgColor: 'rgba(255,172,154,0.12)',
          // 字体颜色
          fontColor: '#e55112',
          // 字体大小
          fontSize: '10px',
          // 宽度：180px
          width: '100px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 0.11,
        },
        { // 边框颜色
          borderColor: '#FFAC9A',
          // 进度颜色
          progressColor: '#e55112',
          // 背景色
          bgColor: 'rgba(255,172,154,0.12)',
          // 字体颜色
          fontColor: '#e55112',
          // 字体大小
          fontSize: '15px',
          // 宽度：180px
          width: '150px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 0.2144,
        },
        { // 边框颜色
          borderColor: '#FFAC9A',
          // 进度颜色
          progressColor: '#e55112',
          // 背景色
          bgColor: 'rgba(255,172,154,0.12)',
          // 字体颜色
          fontColor: '#e55112',
          // 字体大小
          fontSize: '18px',
          // 宽度：180px
          width: '180px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 0.5,
        },
        { // 边框颜色
          borderColor: '#FFAC9A',
          // 进度颜色
          progressColor: '#e55112',
          // 背景色
          bgColor: 'rgba(255,172,154,0.12)',
          // 字体颜色
          fontColor: '#e55112',
          // 字体大小
          fontSize: '20px',
          // 宽度：180px
          width: '200px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 1,
        },

      ]
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  width: 100vw;

}
</style>

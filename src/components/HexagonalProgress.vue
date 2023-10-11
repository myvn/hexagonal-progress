<template>
  <div class="svg-view" :style="{'--width':option.width}">
    <svg class="svg-six-view">
      <!-- 外边 -->
      <polygon :points="pointsOutside "
               :stroke="option.borderColor"
               :stroke-width="sixW*0.007"
               style="fill:transparent;"
      />
      <!-- 内边 -->
      <polygon :points="pointsInside"
               :stroke=" option.borderColor"
               :fill=" option.bgColor"
               :stroke-width="sixW*0.004"
      />
      <!-- 进度线  -->
      <!--      <polyline   :points="processPoints" fill="none" stroke="#0dc1f2" stroke-width="2"/>-->
      <path
          :class="[!pathShow?'':'path']"
          :stroke="option.progressColor"
          :d="processLineD"
          fill="none"
          :stroke-width="sixW*0.032"
      ></path>
      <!-- 修饰线 左边边  -->
      <polyline :points="lineLeftPoints"
                stroke-dasharray="2 2"
                :stroke="option.borderColor"
                :stroke-width="sixW*0.004"
                style="fill:none"
      />
      <!-- 修饰线 右边  -->
      <polyline :points="lineRightPoints"
                stroke-dasharray="2 2"
                :stroke="option.borderColor"
                :stroke-width="sixW*0.004"
                style="fill:none"
      />
    </svg>
    <div class="svg-text-view" :style="{'color': option.fontColor,'--text-font-size':option.fontSize}">
      {{ changeNum }}%
    </div>

  </div>
</template>

<script>
export default {
  name: 'HexagonalProgress',
  props: {
    option: {
      type: Object,
      default() {
        // 边框颜色，进度颜色，背景色
        return {
          // 边框颜色
          borderColor: '#8ee6ff',
          // 进度颜色
          progressColor: '#0dc1f2',
          // 背景色
          bgColor: 'rgba(24,160,206,0.12)',
          // 字体颜色
          fontColor: '#0dc1f2',
          // 字体大小
          fontSize: '16px',
          // 宽度：180px
          width: '180px',
          // 初始角度
          startRad: -120,
          // 进度 （0-1）
          number: 1,
        }
        // return ["#FFAC9A","#e55112","rgba(255,172,154,0.12)"]
      }
    },

    // 边框颜色
    borderColor:  {
      type: String,
      default() {
        return '#8ee6ff'
      }
    },
    // 进度颜色
    progressColor:  {
      type: String,
      default() {
        return '#0dc1f2'
      }
    },
    // 背景色
    bgColor:  {
      type: String,
      default() {
        return 'rgba(24,160,206,0.12)'
      }
    },
    // 字体颜色
    fontColor:  {
      type: String,
      default() {
        return '#0dc1f2'
      }
    },
    // 字体大小
    fontSize: {
      type: String,
      default() {
        return '16px'
      }
    },
    // 宽度
    width: {
      type: String,
      default() {
        return '180px'
      }
    },

    // 初始角度
    startRad: {
      type: Number,
      default() {
        return -120
      }
    },
    // 进度
    number: {
      type: Number,
      default() {
        return 0.4134
      }
    },
  },
  data() {
    return {
      // 动态浮动数字
      changeNum: 0,
      // 六边形宽度
      sixW: 0,
      // 度数
      rad: 60,
      // 外边
      pointsInside: '',
      // 内边
      pointsOutside: '',
      // 外边数组
      arrOutside: [],
      // 内边数组
      arrInside: [],
      // 左边修饰
      lineLeftPoints: '',
      // 右边修饰
      lineRightPoints: '',
      // 进度线
      processPoints: '',
      // 进度数组
      processArr: [],
      // path 动画
      processLineD: '',
      // 路径
      pathShow: false

    }
  },
  watch: {
    number: {
      handler() {
        this.initData()
      },
      immediate: true,
      deep: true
    }

  },
  mounted() {

  },
  methods: {
    // 数字变化
    numberChange() {

      let p = JSON.parse(JSON.stringify(this.option.number))
      p = p > 1 ? 1 : p
      p = p * 100
      let old = p
      let startZS = 0
      let start = 0.01
      if (p !== 0) {
        let sss = setInterval(() => {
          startZS = startZS + 1
          start = start + 0.01
          this.changeNum = (startZS + start).toFixed(2)

          if (start > 1 || startZS > p) {
            this.changeNum = old.toFixed(2)
            clearInterval(sss)
          }
        }, 30)
      }
    },
    //  初始化 六边形数据
    initData() {
      //  六边形宽度
      this.sixW = this.option.width.replace('px', '') * 1

      //  宽度
      let w = this.sixW
      // 几条边
      const numCount = 360 / this.rad
      // 半径  r = 0.5*w - 0.1*w
      let r = (0.5 - 0.1) * w
      // 外边
      let arrOutside = []
      // 内边
      let arrInside = []
      for (let i = 0; i < numCount; i++) {
        arrOutside.push({
          x: this.getPointXY(r, i * this.rad + this.option.startRad).x,
          y: this.getPointXY(r, i * this.rad + this.option.startRad).y
        })
        arrInside.push({
          x: this.getPointXY(r - 0.047 * w, i * this.rad + this.option.startRad).x,
          y: this.getPointXY(r - 0.047 * w, i * this.rad + this.option.startRad).y
        })
      }
      // 外边
      this.arrOutside = arrOutside
      // 内边
      this.arrInside = arrInside
      //  外边点
      this.pointsOutside = arrOutside.map((item) => `${item.x},${item.y}`).join(' ')
      //  内边点
      this.pointsInside = arrInside.map((item) => `${item.x},${item.y}`).join(' ')

      //
      let dr = 0.09 * w
      //  左边修饰
      let { x: x_l_1, y: y_l_1 } = this.getPointXY((r - dr) * Math.cos(2 * Math.PI * 30 / 360), 210)
      let { x: x_l_2, y: y_l_2 } = this.getPointXY(r - dr, 180)
      let { x: x_l_3, y: y_l_3 } = this.getPointXY((r - dr) * Math.cos(2 * Math.PI * 30 / 360), 150)
      this.lineLeftPoints = `${x_l_1},${y_l_1} ${x_l_2},${y_l_2} ${x_l_3},${y_l_3}`

      //  右边修饰
      let { x, y } = this.getPointXY((r - dr) * Math.cos(2 * Math.PI * 30 / 360), -30)
      let { x: x1, y: y1 } = this.getPointXY(r - dr, 0)
      let { x: x2, y: y2 } = this.getPointXY((r - dr) * Math.cos(2 * Math.PI * 30 / 360), 30)
      this.lineRightPoints = `${x},${y} ${x1},${y1} ${x2},${y2}`
      this.processData()
    },
    // 计算进度数据
    processData() {
      this.processLineD = ''
      let r = (0.5 - 0.1) * this.sixW
      // 初始角度
      // 总共度数
      let allJD = this.option.number * 360

      // 商
      let rad_n = Math.ceil(allJD / 60)
      // 余数
      let rad_y = (allJD % 60).toFixed(2) * 1
      if (rad_n !== 0) {
        //商存在
        let n_arr = []

        for (let i = 0; i <= rad_n; i++) {
          n_arr.push({
            x: this.getPointXY(r - this.sixW * 0.024, i * 60 + this.option.startRad).x,
            y: this.getPointXY(r - this.sixW * 0.024, i * 60 + this.option.startRad).y
          })
        }
        // 满进度是偶
        if (allJD === 360) {
          n_arr.push({
            x: this.getPointXY(r - this.sixW * 0.024, 60 + this.option.startRad).x,
            y: this.getPointXY(r - this.sixW * 0.024, 60 + this.option.startRad).y
          })
        }
        // 余数存在
        if (rad_y !== 0) {
          // 余数占60° 多少
          const bl = rad_y / this.rad
          let { length: n_arr_length } = n_arr
          // 倒数第二个点
          let { x: x1, y: y1 } = n_arr[n_arr_length - 2]
          // 最后一个点
          let { x: x2, y: y2 } = n_arr[n_arr_length - 1]
          const x3 = (x2 - x1) * bl + x1
          const y3 = (y2 - y1) * bl + y1
          n_arr[n_arr_length - 1] = { x: x3, y: y3 }
        }

        let dSting = ``
        n_arr.map((item, index) => {
          if (index === 0) {
            dSting += `M${item.x},${item.y}`
          } else {
            dSting += ` L${item.x},${item.y}`
          }
        })
        this.processLineD = dSting
        this.pathShow = true
        setTimeout(() => {
          this.pathShow = false
        }, 1000 * 4)
      }
      this.numberChange()
    },
    // 通过半径 得到点坐标
    getPointXY(r, rad) {
      return {
        x: r * Math.cos((Math.PI * 2 * rad) / 360) + 0.5 * this.sixW,
        y: r * Math.sin((Math.PI * 2 * rad) / 360) + 0.5 * this.sixW
      }
    }

  }
}
</script>

<style scoped lang="scss">
$svgH: var(--width);
$svgHx3: calc(3 * var(--width));
.svg-view {
  display: flex;
  justify-content: center;
  align-items: center;
  width: $svgH;
  height: $svgH;
  position: relative;

  .svg-six-view {
    z-index: 2;
    width: $svgH;
    height: $svgH;
    position: absolute;
  }

  .svg-text-view {
    position: absolute;
    z-index: 1;
    width: $svgH;
    height: $svgH;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: var(--text-font-size);
    font-weight: 500;
  }
}

.path {
  stroke-dasharray: $svgHx3;
  stroke-dashoffset: 0;
  animation: dash 4s linear infinite;
}

@keyframes dash {
  from {
    stroke-dashoffset: $svgHx3;
  }
  to {
    stroke-dashoffset: 0;
  }
}
</style>

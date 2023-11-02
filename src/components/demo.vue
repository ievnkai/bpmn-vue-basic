<!-- 
  演示专用
 -->
<template>
  <div>
    <h1>{{ 'MVP演示专用' }}</h1>
    <!-- 流程画板 -->
    <div class="containers">
      <div class="canvas" ref="canvas"></div>
    </div>
  </div>
</template>

<script>
// 引入 bpmn 的依赖
import BpmnModeler from 'bpmn-js/lib/Modeler'
import { xmlStr } from '../mock/xmlStr';

export default {
  name: 'demo',
  components: {},
  data() {
    return {
      // bpmn建模器
      bpmnModeler: BpmnModeler
    }
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      let canvas = this.$refs.canvas;
      
      // 创建画板实例
      this.bpmnModeler = new BpmnModeler({
        container: canvas,
        palette: {
          filter: this.filterPalette
        }
      });

      this.bpmnModeler.importXML(xmlStr, () => {

      });
    },
    // 隐藏左侧不需要的流程组件
    filterPalette(palette) {
      return {
        'bpmn:ExclusiveGateway': {
          hidden: true
        },
        'bpmn:CallActivity': {
          hidden: true 
        }
      }
    }
  }
}
</script>
<style scoped>
.containers {
	background-color: #ffffff;
	width: 100%;
	height: calc(100vh - 52px);
}

.canvas {
	width: 100%;
	height: 100%;
}

.panel {
	position: absolute;
	right: 0;
	top: 0;
	width: 300px;
}
</style>

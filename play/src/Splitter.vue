<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Splitter Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-splitter
        data-testid="splitter-basic"
        style="width: 500px; height: 200px; border: 1px solid #dcdfe6"
      >
        <el-splitter-panel size="50%">
          <div class="pane">Pane A</div>
        </el-splitter-panel>
        <el-splitter-panel>
          <div class="pane">Pane B</div>
        </el-splitter-panel>
      </el-splitter>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (drag separator)</h3>
      <el-splitter
        data-testid="splitter-interact"
        style="width: 500px; height: 200px; border: 1px solid #dcdfe6"
        @resize="onResize"
      >
        <el-splitter-panel :size="paneSize">
          <div class="pane">Pane A</div>
        </el-splitter-panel>
        <el-splitter-panel>
          <div class="pane">Pane B</div>
        </el-splitter-panel>
      </el-splitter>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ lastSize }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (orientation)</h3>
      <el-button data-testid="splitter-toggle-orientation" @click="vertical = !vertical">
        Toggle orientation: <span data-testid="state-indicator">{{ vertical ? 'vertical' : 'horizontal' }}</span>
      </el-button>
      <el-splitter
        data-testid="splitter-state-target"
        :layout="vertical ? 'vertical' : 'horizontal'"
        style="width: 500px; height: 260px; border: 1px solid #dcdfe6"
      >
        <el-splitter-panel size="50%">
          <div class="pane">Pane A</div>
        </el-splitter-panel>
        <el-splitter-panel>
          <div class="pane">Pane B</div>
        </el-splitter-panel>
      </el-splitter>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const paneSize = ref('50%')
const lastSize = ref(0)
const vertical = ref(false)

function onResize(sizes: number[]) {
  lastSize.value = Math.round(sizes?.[0] ?? 0)
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.pane { height: 100%; width: 100%; padding: 12px; background: #f5f7fa; display: flex; align-items: center; justify-content: center; color: #606266; }
</style>

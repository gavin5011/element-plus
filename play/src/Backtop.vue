<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Backtop Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <!--
        el-backtop is a Vue 3 Fragment-style component (inner <div> is wrapped
        in <transition> with v-if="visible"); attrs set on <el-backtop>
        do not propagate to the rendered <div>. Inject the testid via the
        default slot on el-icon instead — el-icon does v-bind="$attrs" on
        its <i> root, so data-testid + class reach the DOM. Click events on
        the slot child bubble to the floating div's @click.stop="handleClick".
      -->
      <el-backtop :right="40" :bottom="40">
        <el-icon class="el-backtop__icon" data-testid="backtop-basic"
          ><CaretTop
        /></el-icon>
      </el-backtop>
      <div>Scroll page to see back-top button</div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (click to go top)</h3>
      <el-backtop :right="100" :bottom="100" @click="onClick">
        <el-icon class="el-backtop__icon" data-testid="backtop-interact"
          ><CaretTop
        /></el-icon>
      </el-backtop>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ clickCount }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (visibility-height)</h3>
      <el-button
        data-testid="backtop-toggle-visibility"
        @click="highThreshold = !highThreshold"
      >
        Toggle visibility-height:
        <span data-testid="state-indicator">{{
          highThreshold ? '400' : '200'
        }}</span>
      </el-button>
      <el-backtop
        :visibility-height="highThreshold ? 400 : 200"
        :right="160"
        :bottom="160"
      >
        <el-icon class="el-backtop__icon" data-testid="backtop-state-target"
          ><CaretTop
        /></el-icon>
      </el-backtop>
    </section>

    <div class="tall-content">
      Scroll down — tall placeholder content to enable back-top visibility.
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { CaretTop } from '@element-plus/icons-vue'

const clickCount = ref(0)
const highThreshold = ref(false)

function onClick() {
  clickCount.value += 1
}
</script>

<style scoped>
.demo-page {
  padding: 24px;
  font-family: system-ui;
  min-height: 2000px;
}
section {
  margin-top: 16px;
  display: flex;
  gap: 16px;
  align-items: center;
  flex-wrap: wrap;
}
section h3 {
  width: 100%;
  margin-bottom: 8px;
  color: #606266;
}
.tall-content {
  margin-top: 600px;
  color: #909399;
}
</style>

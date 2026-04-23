<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Backtop Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-backtop data-testid="backtop-basic" :right="40" :bottom="40" />
      <div>Scroll page to see back-top button</div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (click to go top)</h3>
      <el-backtop
        data-testid="backtop-interact"
        :right="100"
        :bottom="100"
        @click="onClick"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ clickCount }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (visibility-height)</h3>
      <el-button data-testid="backtop-toggle-visibility" @click="highThreshold = !highThreshold">
        Toggle visibility-height: <span data-testid="state-indicator">{{ highThreshold ? '400' : '200' }}</span>
      </el-button>
      <el-backtop
        data-testid="backtop-state-target"
        :visibility-height="highThreshold ? 400 : 200"
        :right="160"
        :bottom="160"
      />
    </section>

    <div class="tall-content">Scroll down — tall placeholder content to enable back-top visibility.</div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const clickCount = ref(0)
const highThreshold = ref(false)

function onClick() {
  clickCount.value += 1
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; min-height: 2000px; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.tall-content { margin-top: 600px; color: #909399; }
</style>

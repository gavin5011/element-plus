<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tooltip Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tooltip content="Basic tooltip content" placement="top">
        <el-button data-testid="tooltip-basic">Hover me</el-button>
      </el-tooltip>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (hover to show)</h3>
      <el-tooltip
        content="Interact tooltip"
        placement="top"
        @show="onShow"
        @hide="onHide"
      >
        <el-button data-testid="tooltip-interact">Hover for interact</el-button>
      </el-tooltip>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (trigger toggle)</h3>
      <el-button data-testid="tooltip-toggle-trigger" @click="toggleTrigger">
        Toggle trigger: <span data-testid="state-indicator">{{ trigger }}</span>
      </el-button>
      <el-tooltip :content="`Trigger=${trigger}`" :trigger="trigger" placement="top">
        <el-button data-testid="tooltip-state-target">Target</el-button>
      </el-tooltip>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pickedValue = ref('(none)')
const trigger = ref<'hover' | 'click'>('hover')

function onShow() { pickedValue.value = 'shown' }
function onHide() { pickedValue.value = 'hidden' }
function toggleTrigger() {
  trigger.value = trigger.value === 'hover' ? 'click' : 'hover'
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

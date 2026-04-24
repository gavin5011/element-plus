<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">MessageBox Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render (Trigger Button)</h3>
      <el-button data-testid="messagebox-basic" type="primary" @click="openAlert">
        Open Alert
      </el-button>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (confirm / prompt)</h3>
      <el-button data-testid="messagebox-interact" @click="openConfirm">Confirm</el-button>
      <el-button data-testid="messagebox-prompt" @click="openPrompt">Prompt</el-button>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (center-align toggle)</h3>
      <el-button data-testid="messagebox-toggle-center" @click="center = !center">
        Toggle center: <span data-testid="state-indicator">{{ center ? 'center' : 'left' }}</span>
      </el-button>
      <el-button data-testid="messagebox-state-target" @click="openStateAlert">Open state alert</el-button>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElMessageBox } from 'element-plus'

const pickedValue = ref('(none)')
const center = ref(false)

function openAlert() {
  ElMessageBox.alert('This is an alert message', 'Alert').catch(() => {})
}
function openConfirm() {
  ElMessageBox.confirm('Proceed with operation?', 'Confirm')
    .then(() => { pickedValue.value = 'confirmed' })
    .catch(() => { pickedValue.value = 'cancelled' })
}
function openPrompt() {
  ElMessageBox.prompt('Enter value', 'Prompt')
    .then(({ value }) => { pickedValue.value = `prompt:${value}` })
    .catch(() => { pickedValue.value = 'cancelled' })
}
function openStateAlert() {
  ElMessageBox.alert('Centered alert', 'State Alert', { center: center.value }).catch(() => {})
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Message Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render (Trigger Button)</h3>
      <el-button data-testid="message-basic" type="primary" @click="openBasic">
        Show Message
      </el-button>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (success / error / warning)</h3>
      <el-button data-testid="message-interact" type="success" @click="showSuccess">Success</el-button>
      <el-button data-testid="message-error" type="danger" @click="showError">Error</el-button>
      <el-button data-testid="message-warning" type="warning" @click="showWarning">Warning</el-button>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (show-close toggle)</h3>
      <el-button data-testid="message-toggle-close" @click="showClose = !showClose">
        Toggle close: <span data-testid="state-indicator">{{ showClose ? 'with-close' : 'no-close' }}</span>
      </el-button>
      <el-button data-testid="message-state-target" @click="showStateMsg">Show state message</el-button>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElMessage } from 'element-plus'

const pickedValue = ref('(none)')
const showClose = ref(false)

function openBasic() { ElMessage('Basic message') }
function showSuccess() {
  ElMessage.success('Success message')
  pickedValue.value = 'success'
}
function showError() {
  ElMessage.error('Error message')
  pickedValue.value = 'error'
}
function showWarning() {
  ElMessage.warning('Warning message')
  pickedValue.value = 'warning'
}
function showStateMsg() {
  ElMessage({ message: `showClose=${showClose.value}`, showClose: showClose.value })
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

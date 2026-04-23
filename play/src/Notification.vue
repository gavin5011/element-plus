<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Notification Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render (Trigger Button)</h3>
      <el-button data-testid="notification-basic" type="primary" @click="showBasic">
        Show Notification
      </el-button>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (success / error / warning / info)</h3>
      <el-button data-testid="notification-interact" type="success" @click="showSuccess">Success</el-button>
      <el-button data-testid="notification-error" type="danger" @click="showError">Error</el-button>
      <el-button data-testid="notification-warning" type="warning" @click="showWarning">Warning</el-button>
      <el-button data-testid="notification-info" @click="showInfo">Info</el-button>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (position cycle)</h3>
      <el-button data-testid="notification-toggle-position" @click="cyclePosition">
        Toggle position: <span data-testid="state-indicator">{{ position }}</span>
      </el-button>
      <el-button data-testid="notification-state-target" @click="showStateNotif">Show state notification</el-button>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElNotification } from 'element-plus'

const pickedValue = ref('(none)')
const positions = ['top-right', 'top-left', 'bottom-right', 'bottom-left'] as const
type Position = typeof positions[number]
const position = ref<Position>('top-right')

function showBasic() { ElNotification({ title: 'Basic', message: 'Basic notification' }) }
function showSuccess() {
  ElNotification.success({ title: 'Success', message: 'Success notif' })
  pickedValue.value = 'success'
}
function showError() {
  ElNotification.error({ title: 'Error', message: 'Error notif' })
  pickedValue.value = 'error'
}
function showWarning() {
  ElNotification.warning({ title: 'Warning', message: 'Warning notif' })
  pickedValue.value = 'warning'
}
function showInfo() {
  ElNotification.info({ title: 'Info', message: 'Info notif' })
  pickedValue.value = 'info'
}
function cyclePosition() {
  const idx = positions.indexOf(position.value)
  position.value = positions[(idx + 1) % positions.length]
}
function showStateNotif() {
  ElNotification({ title: 'State', message: `Position=${position.value}`, position: position.value })
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

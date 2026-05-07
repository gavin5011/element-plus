<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Notification Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render (Trigger Button)</h3>
      <el-button
        data-testid="notification-basic"
        type="primary"
        @click="showBasic"
      >
        Show Notification
      </el-button>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (success / error / warning / info)</h3>
      <el-button
        data-testid="notification-interact"
        type="success"
        @click="showSuccess"
        >Success</el-button
      >
      <el-button
        data-testid="notification-error"
        type="danger"
        @click="showError"
        >Error</el-button
      >
      <el-button
        data-testid="notification-warning"
        type="warning"
        @click="showWarning"
        >Warning</el-button
      >
      <el-button data-testid="notification-info" @click="showInfo"
        >Info</el-button
      >
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (position cycle)</h3>
      <el-button
        data-testid="notification-toggle-position"
        @click="cyclePosition"
      >
        Toggle position:
        <span data-testid="state-indicator">{{ position }}</span>
      </el-button>
      <el-button data-testid="notification-state-target" @click="showStateNotif"
        >Show state notification</el-button
      >
    </section>

    <section data-testid="scenario-cat6-notification-auto-dismiss">
      <h3>
        S4: cat6 fixture - Notification auto-dismiss timer 1500ms (race vs
        same-session retry)
      </h3>
      <el-button
        data-testid="notification-trigger-auto-dismiss"
        @click="autoDismissHandler"
        >Trigger auto-dismiss notif</el-button
      >
      <div
        v-if="autoDismissShown"
        data-testid="notification-auto-dismiss-card"
        style="border: 1px solid #ccc; padding: 8px; background: #f7f7f7"
      >
        Notification (auto-dismisses 1500ms)
      </div>
    </section>

    <section data-testid="scenario-cat6-notification-delayed-open">
      <h3>
        S5: cat6 fixture - Notification delayed-open 300ms (race vs same-session
        retry)
      </h3>
      <el-button
        data-testid="notification-trigger-delayed-open"
        @click="delayedOpenHandler"
        >Trigger delayed open</el-button
      >
      <div
        v-if="delayedOpenShown"
        data-testid="notification-delayed-open-card"
        style="border: 1px solid #ccc; padding: 8px; background: #f7f7f7"
      >
        Notification (opens 300ms after click)
      </div>
    </section>

    <section data-testid="scenario-cat6-notification-content-update">
      <h3>
        S6: cat6 fixture - Notification content update 200ms (race vs
        same-session retry)
      </h3>
      <el-button
        data-testid="notification-trigger-content-update"
        @click="contentUpdateHandler"
        >Trigger content update</el-button
      >
      <div
        v-if="contentUpdateShown"
        style="border: 1px solid #ccc; padding: 8px; background: #f7f7f7"
      >
        Status:
        <span data-testid="notification-content-update-text">{{
          contentUpdateText
        }}</span>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElNotification } from 'element-plus'

const pickedValue = ref('(none)')
const positions = [
  'top-right',
  'top-left',
  'bottom-right',
  'bottom-left',
] as const
type Position = (typeof positions)[number]
const position = ref<Position>('top-right')

function showBasic() {
  ElNotification({ title: 'Basic', message: 'Basic notification' })
}
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
  ElNotification({
    title: 'State',
    message: `Position=${position.value}`,
    position: position.value,
  })
}

// cat6 fixtures
const autoDismissShown = ref(false)
function autoDismissHandler() {
  autoDismissShown.value = true
  setTimeout(() => {
    autoDismissShown.value = false
  }, 1500)
}

const delayedOpenShown = ref(false)
function delayedOpenHandler() {
  setTimeout(() => {
    delayedOpenShown.value = true
  }, 300)
}

const contentUpdateShown = ref(false)
const contentUpdateText = ref('loading')
function contentUpdateHandler() {
  contentUpdateShown.value = true
  contentUpdateText.value = 'loading'
  setTimeout(() => {
    contentUpdateText.value = 'updated'
  }, 200)
}
</script>

<style scoped>
.demo-page {
  padding: 24px;
  font-family: system-ui;
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
</style>

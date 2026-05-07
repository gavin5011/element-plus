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
      <el-button
        data-testid="message-interact"
        type="success"
        @click="showSuccess"
        >Success</el-button
      >
      <el-button data-testid="message-error" type="danger" @click="showError"
        >Error</el-button
      >
      <el-button
        data-testid="message-warning"
        type="warning"
        @click="showWarning"
        >Warning</el-button
      >
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (show-close toggle)</h3>
      <el-button
        data-testid="message-toggle-close"
        @click="showClose = !showClose"
      >
        Toggle close:
        <span data-testid="state-indicator">{{
          showClose ? 'with-close' : 'no-close'
        }}</span>
      </el-button>
      <el-button data-testid="message-state-target" @click="showStateMsg"
        >Show state message</el-button
      >
    </section>

    <section data-testid="scenario-cat6-show-after-delay">
      <h3>
        S4: cat6 fixture — Message show-after-delay race (50ms setTimeout vs
        tight assertion)
      </h3>
      <p>
        Click the trigger to schedule a custom toast via `setTimeout(showMsg,
        50ms)`. Spec assertion uses tight 30ms timeout — first attempt fails
        (timer not fired), same-session retry passes (~60ms wait between
        attempts gives setTimeout time to fire). cat6 flake fixture
        (deterministic-looking timing race).
      </p>
      <el-button
        data-testid="cat6-message-trigger"
        type="primary"
        @click="cat6Trigger"
      >
        Show toast after 50ms delay
      </el-button>
      <!-- Custom toast element (not ElMessage) so spec can assert visibility deterministically -->
      <Transition name="fade">
        <div
          v-if="cat6Visible"
          data-testid="cat6-message-toast"
          class="cat6-toast"
        >
          Delayed toast (50ms after trigger)
        </div>
      </Transition>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ElMessage } from 'element-plus'

const pickedValue = ref('(none)')
const showClose = ref(false)
const cat6Visible = ref(false)

function openBasic() {
  ElMessage('Basic message')
}
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
  ElMessage({
    message: `showClose=${showClose.value}`,
    showClose: showClose.value,
  })
}
function cat6Trigger() {
  // 50ms setTimeout — first spec assertion at 30ms timeout misses,
  // same-session retry (60ms wait) passes.
  cat6Visible.value = false
  setTimeout(() => {
    cat6Visible.value = true
  }, 50)
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
.cat6-toast {
  margin-left: 16px;
  padding: 8px 16px;
  background: #f0f9eb;
  border: 1px solid #67c23a;
  border-radius: 4px;
  color: #67c23a;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.15s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

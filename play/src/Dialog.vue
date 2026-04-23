<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Dialog Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render (Trigger Button)</h3>
      <el-button data-testid="btn-open-dialog" type="primary" @click="visible = true">
        Open Dialog
      </el-button>
      <div data-testid="dialog-state">State: {{ visible ? 'open' : 'closed' }}</div>
    </section>

    <el-dialog
      v-model="visible"
      title="Confirmation Dialog"
      width="420"
      data-testid="dialog-root"
    >
      <div data-testid="dialog-body">
        <p>Are you sure you want to proceed?</p>
        <p>Message count: <span data-testid="dialog-count">{{ acks }}</span></p>
      </div>
      <template #footer>
        <el-button data-testid="btn-cancel" @click="visible = false">Cancel</el-button>
        <el-button data-testid="btn-confirm" type="primary" @click="confirm">
          Confirm
        </el-button>
      </template>
    </el-dialog>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → Confirm → Close)</h3>
      <div data-testid="last-action">Last action: {{ lastAction }}</div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (fullscreen toggle — observable without opening)</h3>
      <el-button data-testid="dialog-toggle-fullscreen" @click="fullscreen = !fullscreen">
        Toggle fullscreen: <span data-testid="state-indicator">{{ fullscreen ? 'fullscreen' : 'normal' }}</span>
      </el-button>
      <el-button data-testid="dialog-open-state" @click="stateVisible = true">Open state dialog</el-button>
      <el-dialog
        v-model="stateVisible"
        :fullscreen="fullscreen"
        title="State Dialog"
        data-testid="dialog-state-target"
      >
        <p>Fullscreen prop: {{ fullscreen }}</p>
        <template #footer>
          <el-button data-testid="btn-close-state" @click="stateVisible = false">Close</el-button>
        </template>
      </el-dialog>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const visible = ref(false)
const acks = ref(0)
const lastAction = ref('(none)')
function confirm() {
  acks.value++
  lastAction.value = `confirmed @ ${new Date().toISOString()}`
  visible.value = false
}

const fullscreen = ref(false)
const stateVisible = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Drawer Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render (Trigger Button)</h3>
      <el-button data-testid="drawer-basic" type="primary" @click="basicVisible = true">
        Open Drawer
      </el-button>
      <div data-testid="drawer-state">State: {{ basicVisible ? 'open' : 'closed' }}</div>
    </section>

    <el-drawer
      v-model="basicVisible"
      title="Basic Drawer"
      data-testid="drawer-basic-root"
    >
      <p>Basic drawer content</p>
    </el-drawer>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → Close)</h3>
      <el-button data-testid="drawer-interact" @click="openInteract">Open Interact Drawer</el-button>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <el-drawer
      v-model="interactVisible"
      title="Interact Drawer"
      data-testid="drawer-interact-root"
    >
      <p>Click close to update value</p>
      <el-button data-testid="drawer-close" @click="closeInteract">Close</el-button>
    </el-drawer>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (direction cycle)</h3>
      <el-button data-testid="drawer-toggle-direction" @click="cycleDirection">
        Toggle direction: <span data-testid="state-indicator">{{ direction }}</span>
      </el-button>
      <el-button data-testid="drawer-state-target" @click="stateVisible = true">Open state drawer</el-button>
      <el-drawer
        data-testid="drawer-state-root"
        v-model="stateVisible"
        :direction="direction"
        title="State Drawer"
      >
        <p>Direction: {{ direction }}</p>
      </el-drawer>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicVisible = ref(false)
const interactVisible = ref(false)
const pickedValue = ref('(none)')
const stateVisible = ref(false)
const directions = ['ltr', 'rtl', 'ttb', 'btt'] as const
type Direction = typeof directions[number]
const direction = ref<Direction>('rtl')

function openInteract() {
  interactVisible.value = true
  pickedValue.value = 'opened'
}
function closeInteract() {
  interactVisible.value = false
  pickedValue.value = 'closed'
}
function cycleDirection() {
  const idx = directions.indexOf(direction.value)
  direction.value = directions[(idx + 1) % directions.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

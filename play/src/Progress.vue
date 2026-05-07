<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Progress Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-progress data-testid="progress-basic" :percentage="40" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (increment)</h3>
      <el-button data-testid="progress-increment" @click="incrementPct"
        >Increment</el-button
      >
      <el-progress data-testid="progress-interact" :percentage="pickedValue" />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (line / circle / dashboard)</h3>
      <el-button data-testid="progress-toggle-type" @click="cycleType">
        Toggle type:
        <span data-testid="state-indicator">{{ progressType }}</span>
      </el-button>
      <el-progress
        data-testid="progress-state-target"
        :percentage="60"
        :type="progressType"
      />
    </section>

    <section data-testid="scenario-cat2-progress-rendering">
      <h3>
        S4: cat2 fixture — Progress bar rendering pixel diff (active CSS
        rendering mutation)
      </h3>
      <p>
        Active CSS mutation on the inner bar: `transform: scaleX(0.95)
        translateZ(0)`. Functional behavior unchanged (aria-valuenow and
        percentage text correct). Visual screenshot diff present (small
        deterministic width rendering diff). cat2 = visual-only diff in
        supported environment.
      </p>
      <div
        class="cat2-progress-wrapper"
        data-testid="cat2-progress-bar-wrapper"
        :aria-valuenow="60"
        style="width: 320px"
      >
        <el-progress
          data-testid="cat2-progress-bar"
          :percentage="60"
          :stroke-width="14"
          :show-text="true"
          aria-valuenow="60"
        />
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pickedValue = ref(40)
const progressType = ref<'line' | 'circle' | 'dashboard'>('line')

function incrementPct() {
  pickedValue.value = Math.min(100, pickedValue.value + 10)
}

function cycleType() {
  const order: Array<'line' | 'circle' | 'dashboard'> = [
    'line',
    'circle',
    'dashboard',
  ]
  const idx = order.indexOf(progressType.value)
  progressType.value = order[(idx + 1) % order.length]
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
/* cat2 mutation: small deterministic width rendering diff vs baseline screenshot.
   Functional behavior unchanged (aria-valuenow + percentage text remain correct). */
.cat2-progress-wrapper :deep(.el-progress-bar__inner) {
  transform: scaleX(0.95) translateZ(0);
  transform-origin: left center;
}
</style>

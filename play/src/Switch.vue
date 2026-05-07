<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Switch Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-switch data-testid="switch-basic" v-model="basicValue" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (toggle on/off)</h3>
      <el-switch data-testid="switch-interact" v-model="pickedValue" />
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue ? 'on' : 'off' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (loading toggle)</h3>
      <el-button
        data-testid="switch-toggle-loading"
        @click="loading = !loading"
      >
        Toggle loading:
        <span data-testid="state-indicator">{{
          loading ? 'loading' : 'idle'
        }}</span>
      </el-button>
      <el-switch
        data-testid="switch-state-target"
        v-model="stateValue"
        :loading="loading"
      />
    </section>

    <section data-testid="scenario-cat1-active-text">
      <h3>
        S5: cat1 fixture — active-text label mismatch (synthetic seeded bug)
      </h3>
      <el-switch
        data-testid="switch-activetext-bug"
        :model-value="true"
        :disabled="true"
      />
      <div data-testid="picked-value-display">
        Label text (state=ON, should be 'ON'):
        <span data-testid="picked-value">{{ buggyActiveLabel }}</span>
      </div>
    </section>

    <section data-testid="scenario-cat1-vmodel-bug">
      <h3>
        S4: cat1 fixture — switch v-model state mismatch (synthetic seeded bug)
      </h3>
      <el-switch
        data-testid="switch-vmodel-bug"
        :model-value="bugSwitchView"
        @update:model-value="onBugSwitchUpdate"
      />
      <div data-testid="picked-value-display">
        Switch state (should track click events):
        <span data-testid="picked-value">{{ String(bugSwitchView) }}</span>
      </div>
    </section>

    <section data-testid="scenario-cat4-switch-wrapper">
      <h3>
        S4: cat4 fixture - Switch testid moved to wrapper (post-freeze refactor)
      </h3>
      <p>
        Spec was frozen with selector <code>data-testid="switch-root"</code> on
        the el-switch root element. UI refactor moved the testid to the parent
        wrapper div <code>data-testid="cat4-switch-wrapper-switch-wrap"</code>.
        Spec selector no longer resolves.
      </p>
      <div data-testid="cat4-switch-wrapper-switch-wrap" class="switch-wrap">
        <el-switch v-model="cat4WrapperSwitch" />
      </div>
    </section>

    <section data-testid="scenario-cat1-switch-inversion">
      <h3>S5: cat1 fixture - Switch state inversion</h3>
      <p>Click toggle: handler is inverted, state stays at "off".</p>
      <el-button
        data-testid="cat1-switch-inversion-trigger"
        @click="cat1SwitchToggle"
        >Click</el-button
      >
      <span
        >State:
        <span data-testid="cat1-switch-inversion-state">{{
          cat1SwitchState
        }}</span></span
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref(false)
const pickedValue = ref(false)
const stateValue = ref(true)
const loading = ref(false)
const cat4WrapperSwitch = ref(false)

// Synthetic seeded bug: model value updates ignore click events.
// Expected: bugSwitchView toggles on click
// Actual: bugSwitchView stays false regardless of click
const bugSwitchView = ref(false)
function onBugSwitchUpdate(_v: boolean) {
  // BUG: should set bugSwitchView.value = _v but doesn't
}

// Synthetic seeded bug: switch state=ON but exposed label says 'OFF'.
// Expected: 'ON'
// Actual: 'OFF'
const buggyActiveLabel = ref<string>('OFF')

const cat1SwitchState = ref('off')
function cat1SwitchToggle() {
  // Inverted bug: should set to 'on' but sets to 'off'
  cat1SwitchState.value = 'off'
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

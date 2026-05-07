<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">InputNumber Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-input-number
        data-testid="input-number-basic"
        v-model="basicValue"
        :min="0"
        :max="100"
        :step="1"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (increment/decrement)</h3>
      <el-input-number
        data-testid="input-number-interact"
        v-model="pickedValue"
        :min="0"
        :max="100"
        :step="1"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (precision toggle)</h3>
      <el-button
        data-testid="input-number-toggle-precision"
        @click="highPrecision = !highPrecision"
      >
        Toggle precision:
        <span data-testid="state-indicator">{{
          highPrecision ? '2 decimals' : '0 decimals'
        }}</span>
      </el-button>
      <el-input-number
        data-testid="input-number-state-target"
        v-model="stateValue"
        :min="0"
        :max="100"
        :step="highPrecision ? 0.01 : 1"
        :precision="highPrecision ? 2 : 0"
      />
    </section>

    <section data-testid="scenario-cat6-compute">
      <h3>S4: Async compute (cat 6 fixture)</h3>
      <el-button data-testid="input-number-compute" @click="startCompute"
        >Compute</el-button
      >
      <div data-testid="picked-value-display">
        Result: <span data-testid="picked-value">{{ computeResult }}</span>
      </div>
    </section>

    <section data-testid="scenario-cat1-input-number-min">
      <h3>S5: cat1 fixture - InputNumber min boundary inversion</h3>
      <p>Click "Set 30" (min=0): handler clamps to min.</p>
      <el-button
        data-testid="cat1-input-number-set-30"
        @click="cat1InputNumberSet30"
        >Set 30</el-button
      >
      <span
        >Value:
        <span data-testid="cat1-input-number-value">{{
          cat1InputNumberValue
        }}</span></span
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref(10)
const pickedValue = ref(0)
const stateValue = ref(5)
const highPrecision = ref(false)
const computeResult = ref<string>('idle')
function startCompute() {
  computeResult.value = 'pending'
  setTimeout(() => {
    computeResult.value = 'computed'
  }, 1000)
}

const cat1InputNumberValue = ref(0)
function cat1InputNumberSet30() {
  // Bug: should set 30 but inverted-clamp logic forces to min=0
  cat1InputNumberValue.value = 0
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

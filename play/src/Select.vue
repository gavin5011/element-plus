<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Select Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-select
        data-testid="select-basic"
        v-model="basicValue"
        placeholder="Pick a fruit"
      >
        <el-option
          v-for="o in options"
          :key="o.value"
          :label="o.label"
          :value="o.value"
        />
      </el-select>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → pick)</h3>
      <el-select
        data-testid="select-interact"
        v-model="pickedValue"
        placeholder="Select one"
        clearable
      >
        <el-option
          v-for="o in options"
          :key="o.value"
          :label="o.label"
          :value="o.value"
        />
      </el-select>
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (multiple toggle)</h3>
      <el-button
        data-testid="select-toggle-multiple"
        @click="toggleMultipleState"
      >
        Toggle mode:
        <span data-testid="state-indicator">{{
          multiple ? 'multiple' : 'single'
        }}</span>
      </el-button>
      <el-select
        data-testid="select-state-target"
        v-model="stateValue"
        :multiple="multiple"
        placeholder="State-variant"
      >
        <el-option
          v-for="o in options"
          :key="o.value"
          :label="o.label"
          :value="o.value"
        />
      </el-select>
    </section>

    <section data-testid="scenario-cat3-select-fixed-pos">
      <h3>cat3 fixture - Select fixed-positioning mismatch coupling</h3>
      <p>
        Visual mutation creates overlay/clip; functional click
        intercepted/clipped.
      </p>
      <div style="position: relative; display: inline-block">
        <el-button data-testid="cat3-select-option-A">Option A</el-button>
        <div
          style="
            position: absolute;
            inset: 0;
            background: rgba(0, 255, 0, 0.05);
            pointer-events: auto;
            z-index: 10;
          "
        ></div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const options = [
  { value: 'apple', label: 'Apple' },
  { value: 'banana', label: 'Banana' },
  { value: 'cherry', label: 'Cherry' },
  { value: 'date', label: 'Date' },
  { value: 'elderberry', label: 'Elderberry' },
]

const basicValue = ref('')
const pickedValue = ref('')
const multiple = ref(false)
const stateValue = ref<string | string[]>('')

function toggleMultipleState() {
  multiple.value = !multiple.value
  stateValue.value = multiple.value ? [] : ''
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

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">DatePicker Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <div data-testid="picker-basic">
        <el-date-picker v-model="dateA" type="date" placeholder="Select date" />
      </div>
      <div data-testid="picker-range">
        <el-date-picker
          v-model="dateRange"
          type="daterange"
          range-separator="to"
          start-placeholder="Start"
          end-placeholder="End"
        />
      </div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open picker, select date)</h3>
      <div data-testid="picker-interact">
        <el-date-picker
          v-model="pickedDate"
          type="date"
          placeholder="Pick a date"
          format="YYYY-MM-DD"
          value-format="YYYY-MM-DD"
        />
      </div>
      <div data-testid="picked-value">
        Picked:
        <span data-testid="picked-string">{{ pickedDate || '(none)' }}</span>
      </div>
      <el-button data-testid="btn-clear-date" @click="pickedDate = ''"
        >Clear</el-button
      >
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (picker type cycle)</h3>
      <el-button data-testid="picker-cycle-type" @click="cyclePickerType">
        Cycle type:
        <span data-testid="state-indicator">{{ currentPickerType }}</span>
      </el-button>
      <div data-testid="picker-state-target">
        <el-date-picker
          :type="currentPickerType"
          v-model="stateValue"
          placeholder="State-variant"
        />
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const dateA = ref('')
const dateRange = ref<[string, string] | null>(null)
const pickedDate = ref('')

const pickerTypes = ['date', 'datetime', 'month'] as const
type PickerType = (typeof pickerTypes)[number]
const currentPickerType = ref<PickerType>('date')
const stateValue = ref('')
function cyclePickerType() {
  const i = pickerTypes.indexOf(currentPickerType.value)
  currentPickerType.value = pickerTypes[(i + 1) % pickerTypes.length]
  stateValue.value = ''
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

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

    <section data-testid="scenario-cat1-clear-bug">
      <h3>S5: cat1 fixture — clear button broken (synthetic seeded bug)</h3>
      <el-button data-testid="datepicker-set-then-clear" @click="setThenClear">
        Set 2026-02-20 then Clear
      </el-button>
      <div data-testid="picked-value-display">
        Stored value (should be empty after clear): "<span
          data-testid="picked-value"
          >{{ bugClearValue }}</span
        >"
      </div>
    </section>

    <section data-testid="scenario-cat1-format-bug">
      <h3>S4: cat1 fixture — date format mismatch (synthetic seeded bug)</h3>
      <el-button data-testid="datepicker-set-fixed" @click="setFixedDate">
        Set 2026-01-15
      </el-button>
      <div data-testid="picked-value-display">
        Stored value (should be ISO YYYY-MM-DD):
        <span data-testid="picked-value">{{ bugDateValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-cat4-date-picker-year-rename">
      <h3>
        S4: cat4 fixture - DatePicker year-cell testid rename (post-freeze
        refactor)
      </h3>
      <p>
        Spec was frozen with selector <code>data-testid="year-2024"</code>. UI
        refactor renamed to
        <code>data-testid="cat4-date-picker-year-rename-year-cell-2024"</code>.
        Spec selector no longer resolves.
      </p>
      <div class="cat4-year-cell-row">
        <span data-testid="cat4-date-picker-year-rename-year-cell-2024"
          >2024 (renamed from year-2024)</span
        >
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

// Synthetic seeded bug: button stores date in MM/DD/YYYY format instead of ISO YYYY-MM-DD.
// Expected: bugDateValue === '2026-01-15'
// Actual: bugDateValue === '01/15/2026'
const bugDateValue = ref('(none)')
function setFixedDate() {
  // BUG: should store '2026-01-15' but stores US format
  bugDateValue.value = '01/15/2026'
}

// Synthetic seeded bug: clear button stores intermediate value but doesn't clear.
// Expected: bugClearValue = '' after clear
// Actual: bugClearValue = '2026-02-20' (set value, then ignore clear)
const bugClearValue = ref('')
function setThenClear() {
  bugClearValue.value = '2026-02-20'
  // BUG: clear step missing — value remains
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

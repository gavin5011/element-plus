<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Calendar Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-calendar data-testid="calendar-basic" v-model="basicDate" style="width: 600px" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (pick date)</h3>
      <el-calendar data-testid="calendar-interact" v-model="pickedDate" style="width: 600px" />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedDateLabel }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (first day of week)</h3>
      <el-button data-testid="calendar-toggle-firstdayofweek" @click="mondayFirst = !mondayFirst">
        Toggle first day: <span data-testid="state-indicator">{{ mondayFirst ? 'monday' : 'sunday' }}</span>
      </el-button>
      <el-calendar
        data-testid="calendar-state-target"
        v-model="stateDate"
        :first-day-of-week="mondayFirst ? 1 : 7"
        style="width: 600px"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

const basicDate = ref(new Date(2026, 3, 15))
const pickedDate = ref(new Date(2026, 3, 15))
const mondayFirst = ref(true)
const stateDate = ref(new Date(2026, 3, 15))

const pickedDateLabel = computed(() => {
  const d = pickedDate.value
  if (!d) return '(none)'
  return `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}-${String(d.getDate()).padStart(2, '0')}`
})
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

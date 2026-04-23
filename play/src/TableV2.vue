<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">TableV2 Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <div style="width: 600px; height: 300px;">
        <el-table-v2
          data-testid="tablev2-basic"
          :columns="columns"
          :data="rows"
          :width="600"
          :height="300"
        />
      </div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click row)</h3>
      <div style="width: 600px; height: 300px;">
        <el-table-v2
          data-testid="tablev2-interact"
          :columns="columns"
          :data="rows"
          :width="600"
          :height="300"
          :row-event-handlers="{ onClick: onRowClick }"
        />
      </div>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (sortBy toggle)</h3>
      <el-button data-testid="tablev2-toggle-sortBy" @click="toggleSort">
        Toggle sortBy: <span data-testid="state-indicator">{{ sortKey }}</span>
      </el-button>
      <div style="width: 600px; height: 300px;">
        <el-table-v2
          data-testid="tablev2-state-target"
          :columns="columns"
          :data="sortedRows"
          :width="600"
          :height="300"
          :sort-by="{ key: sortKey, order: 'asc' }"
        />
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

type Row = { id: number; name: string; country: string; age: number }

const columns = [
  { key: 'id', dataKey: 'id', title: 'ID', width: 80 },
  { key: 'name', dataKey: 'name', title: 'Name', width: 180 },
  { key: 'country', dataKey: 'country', title: 'Country', width: 180 },
  { key: 'age', dataKey: 'age', title: 'Age', width: 120 },
]

const countries = ['JP', 'CN', 'US', 'DE', 'FR', 'BR']
const rows: Row[] = Array.from({ length: 200 }, (_, i) => ({
  id: i,
  name: `Name ${i}`,
  country: countries[i % countries.length],
  age: 20 + (i % 50),
}))

const pickedValue = ref('')
const sortKey = ref<'id' | 'name' | 'country' | 'age'>('id')

const sortedRows = computed(() => {
  const copy = [...rows]
  const k = sortKey.value
  copy.sort((a, b) => (a[k] > b[k] ? 1 : a[k] < b[k] ? -1 : 0))
  return copy
})

function toggleSort() {
  const order: Array<'id' | 'name' | 'country' | 'age'> = ['id', 'name', 'country', 'age']
  const idx = order.indexOf(sortKey.value)
  sortKey.value = order[(idx + 1) % order.length]
}

function onRowClick(payload: { rowData: Row }) {
  pickedValue.value = payload.rowData?.name ?? ''
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

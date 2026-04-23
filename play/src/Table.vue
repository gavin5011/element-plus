<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Table Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-table
        data-testid="table-basic"
        :data="rows"
        style="width: 100%"
        :border="true"
      >
        <el-table-column prop="date" label="Date" width="140" />
        <el-table-column prop="name" label="Name" width="160" />
        <el-table-column prop="amount" label="Amount" width="120" sortable />
        <el-table-column prop="address" label="Address" />
      </el-table>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Sort + Row Select)</h3>
      <div data-testid="selected-info">
        Selected: <span data-testid="selected-name">{{ selectedName }}</span>
      </div>
      <el-table
        data-testid="table-interact"
        :data="rows"
        style="width: 100%"
        highlight-current-row
        @current-change="onCurrentChange"
      >
        <el-table-column prop="name" label="Name" width="160" />
        <el-table-column prop="amount" label="Amount" width="120" sortable />
        <el-table-column prop="address" label="Address" />
      </el-table>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (loading toggle)</h3>
      <el-button data-testid="table-toggle-loading" @click="tableLoading = !tableLoading">
        Toggle loading: <span data-testid="state-indicator">{{ tableLoading ? 'loading' : 'idle' }}</span>
      </el-button>
      <el-table
        data-testid="table-state-target"
        :data="rows"
        v-loading="tableLoading"
        style="width: 100%"
      >
        <el-table-column prop="name" label="Name" width="160" />
        <el-table-column prop="amount" label="Amount" width="120" />
      </el-table>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Row = { date: string; name: string; amount: number; address: string }

const rows = ref<Row[]>([
  { date: '2026-04-01', name: 'Alice', amount: 120, address: '1 Main St' },
  { date: '2026-04-02', name: 'Bob', amount: 80,  address: '2 Oak Ave' },
  { date: '2026-04-03', name: 'Carol', amount: 250, address: '3 Elm Rd' },
  { date: '2026-04-04', name: 'Dave', amount: 45,  address: '4 Pine Ln' },
])

const selectedName = ref('(none)')
function onCurrentChange(row: Row | null) {
  selectedName.value = row ? row.name : '(none)'
}

const tableLoading = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; }
section h3 { margin-bottom: 8px; color: #606266; }
</style>

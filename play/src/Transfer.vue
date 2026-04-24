<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Transfer Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-transfer
        data-testid="transfer-basic"
        v-model="basicValue"
        :data="items"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (move items left/right)</h3>
      <el-transfer
        data-testid="transfer-interact"
        v-model="pickedValue"
        :data="items"
        :button-texts="['Move to left', 'Move to right']"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue.join(', ') || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (filterable toggle)</h3>
      <el-button data-testid="transfer-toggle-filterable" @click="filterable = !filterable">
        Toggle filterable: <span data-testid="state-indicator">{{ filterable ? 'filterable' : 'plain' }}</span>
      </el-button>
      <el-transfer
        data-testid="transfer-state-target"
        v-model="stateValue"
        :data="items"
        :filterable="filterable"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Item = { key: number; label: string; disabled?: boolean }

const items: Item[] = [
  { key: 1, label: 'Item 1' },
  { key: 2, label: 'Item 2' },
  { key: 3, label: 'Item 3' },
  { key: 4, label: 'Item 4' },
  { key: 5, label: 'Item 5' },
  { key: 6, label: 'Item 6' },
]

const basicValue = ref<number[]>([])
const pickedValue = ref<number[]>([])
const stateValue = ref<number[]>([])
const filterable = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">TreeSelect Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tree-select
        data-testid="treeselect-basic"
        v-model="basicValue"
        :data="treeData"
        placeholder="Pick a region"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → pick)</h3>
      <el-tree-select
        data-testid="treeselect-interact"
        v-model="pickedValue"
        :data="treeData"
        placeholder="Pick one"
        clearable
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (checkable toggle)</h3>
      <el-button data-testid="treeselect-toggle-checkable" @click="checkable = !checkable; stateValue = checkable ? [] : ''">
        Toggle checkable: <span data-testid="state-indicator">{{ checkable ? 'checkable' : 'single' }}</span>
      </el-button>
      <el-tree-select
        data-testid="treeselect-state-target"
        v-model="stateValue"
        :data="treeData"
        :show-checkbox="checkable"
        :multiple="checkable"
        placeholder="State-variant"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Node = { value: string; label: string; children?: Node[] }

const treeData: Node[] = [
  {
    value: 'asia', label: 'Asia',
    children: [
      { value: 'jp', label: 'Japan', children: [
        { value: 'tokyo', label: 'Tokyo' },
        { value: 'osaka', label: 'Osaka' },
      ] },
      { value: 'cn', label: 'China', children: [
        { value: 'beijing', label: 'Beijing' },
        { value: 'shanghai', label: 'Shanghai' },
      ] },
    ],
  },
  {
    value: 'europe', label: 'Europe',
    children: [
      { value: 'de', label: 'Germany', children: [
        { value: 'berlin', label: 'Berlin' },
        { value: 'munich', label: 'Munich' },
      ] },
      { value: 'fr', label: 'France', children: [
        { value: 'paris', label: 'Paris' },
        { value: 'lyon', label: 'Lyon' },
      ] },
    ],
  },
]

const basicValue = ref('')
const pickedValue = ref('')
const checkable = ref(false)
const stateValue = ref<string | string[]>('')
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

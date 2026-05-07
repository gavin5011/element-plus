<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Cascader Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <div data-testid="cascader-basic">
        <el-cascader
          v-model="basicValue"
          :options="options"
          placeholder="Select region"
        />
      </div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → select path)</h3>
      <div data-testid="cascader-interact">
        <el-cascader
          v-model="pickedPath"
          :options="options"
          placeholder="Pick a path"
          :props="{ expandTrigger: 'hover' }"
          clearable
        />
      </div>
      <div data-testid="picked-path-display">
        Picked:
        <span data-testid="picked-path-value">{{
          pickedPath.join(' / ') || '(none)'
        }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (disabled toggle)</h3>
      <el-button
        data-testid="cascader-toggle-disabled"
        @click="cascaderDisabled = !cascaderDisabled"
      >
        Toggle disabled:
        <span data-testid="state-indicator">{{
          cascaderDisabled ? 'disabled' : 'enabled'
        }}</span>
      </el-button>
      <div data-testid="cascader-state-target">
        <el-cascader
          :options="options"
          :disabled="cascaderDisabled"
          v-model="stateValue"
          placeholder="State-variant"
        />
      </div>
    </section>

    <section data-testid="scenario-cat4-cascader-leaf-casing">
      <h3>
        S4: cat4 fixture - Cascader leaf testid casing change (post-freeze
        refactor)
      </h3>
      <p>
        Spec was frozen with selector
        <code>data-testid="cascader-option-itemA"</code> (camelCase). UI
        refactor changed to kebab-case
        <code
          >data-testid="cat4-cascader-leaf-casing-cascader-option-item-a"</code
        >. Spec selector no longer resolves.
      </p>
      <div class="cat4-cascader-leaf-row">
        <span data-testid="cat4-cascader-leaf-casing-cascader-option-item-a"
          >item-a (renamed from itemA)</span
        >
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Option = { value: string; label: string; children?: Option[] }

const options: Option[] = [
  {
    value: 'asia',
    label: 'Asia',
    children: [
      {
        value: 'jp',
        label: 'Japan',
        children: [
          { value: 'tokyo', label: 'Tokyo' },
          { value: 'kyoto', label: 'Kyoto' },
        ],
      },
      {
        value: 'cn',
        label: 'China',
        children: [
          { value: 'beijing', label: 'Beijing' },
          { value: 'shanghai', label: 'Shanghai' },
        ],
      },
    ],
  },
  {
    value: 'europe',
    label: 'Europe',
    children: [
      {
        value: 'de',
        label: 'Germany',
        children: [
          { value: 'berlin', label: 'Berlin' },
          { value: 'munich', label: 'Munich' },
        ],
      },
      {
        value: 'fr',
        label: 'France',
        children: [
          { value: 'paris', label: 'Paris' },
          { value: 'lyon', label: 'Lyon' },
        ],
      },
    ],
  },
]

const basicValue = ref<string[]>([])
const pickedPath = ref<string[]>([])
const cascaderDisabled = ref(false)
const stateValue = ref<string[]>([])
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

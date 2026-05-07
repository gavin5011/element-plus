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

    <section
      data-testid="scenario-cat3-cascader-transform-zorder"
      style="position: relative"
    >
      <h3>S5: cat3 fixture - Cascader transform z-order coupling</h3>
      <p>
        Transform creates new stacking context; overlay div intercepts clicks.
      </p>
      <div style="position: relative; display: inline-block">
        <el-button data-testid="cat3-cascader-transform-leaf"
          >Cascader leaf</el-button
        >
        <div
          style="
            position: absolute;
            inset: 0;
            background: rgba(255, 0, 0, 0.05);
            pointer-events: auto;
            z-index: 10;
            transform: translateZ(0);
          "
        ></div>
      </div>
    </section>

    <section data-testid="scenario-cat5-structured-clone">
      <h3>
        S6: cat5 fixture - structuredClone capability gap (Chrome 98+ only)
      </h3>
      <p>
        Click triggers structuredClone() on a sample object. Older browsers
        throw ReferenceError.
      </p>
      <el-button
        data-testid="cat5-structured-clone-trigger"
        @click="cat5StructuredCloneHandler"
        >Clone</el-button
      >
      <span
        >Result:
        <span data-testid="cat5-structured-clone-result">{{
          cat5StructuredCloneResult
        }}</span></span
      >
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

const cat5StructuredCloneResult = ref('idle')
function cat5StructuredCloneHandler() {
  try {
    // structuredClone is unsupported in Chrome <98 / Edge <99
    // @ts-expect-error: intentional capability probe
    const cloned = structuredClone({ a: 1, nested: { b: 2 } })
    if (cloned.nested.b === 2)
      cat5StructuredCloneResult.value = 'cloned-success'
  } catch (e) {
    cat5StructuredCloneResult.value = 'error: ' + (e as Error).message
  }
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

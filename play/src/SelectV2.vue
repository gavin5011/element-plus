<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">SelectV2 Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-select-v2
        data-testid="selectv2-basic"
        v-model="basicValue"
        :options="options"
        placeholder="Pick an item"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Open → pick)</h3>
      <el-select-v2
        data-testid="selectv2-interact"
        v-model="pickedValue"
        :options="options"
        placeholder="Pick one"
        clearable
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (multiple toggle)</h3>
      <el-button data-testid="selectv2-toggle-multiple" @click="multiple = !multiple; stateValue = multiple ? [] : ''">
        Toggle mode: <span data-testid="state-indicator">{{ multiple ? 'multiple' : 'single' }}</span>
      </el-button>
      <el-select-v2
        data-testid="selectv2-state-target"
        v-model="stateValue"
        :options="options"
        :multiple="multiple"
        placeholder="State-variant"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const options = Array.from({ length: 100 }, (_, i) => ({
  value: `item-${i}`,
  label: `Item ${i}`,
}))

const basicValue = ref('')
const pickedValue = ref('')
const multiple = ref(false)
const stateValue = ref<string | string[]>('')
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

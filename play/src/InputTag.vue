<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">InputTag Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-input-tag
        data-testid="input-tag-basic"
        v-model="basicValue"
        placeholder="Add tags"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (add/remove tag)</h3>
      <el-input-tag
        data-testid="input-tag-interact"
        v-model="pickedValue"
        placeholder="Type and Enter"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue.join(', ') || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (max tag limit)</h3>
      <el-button data-testid="input-tag-toggle-max" @click="limited = !limited">
        Toggle max: <span data-testid="state-indicator">{{ limited ? 'max 3' : 'unlimited' }}</span>
      </el-button>
      <el-input-tag
        data-testid="input-tag-state-target"
        v-model="stateValue"
        :max="limited ? 3 : undefined"
        placeholder="Add tags"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref<string[]>(['Tag1', 'Tag2'])
const pickedValue = ref<string[]>([])
const stateValue = ref<string[]>([])
const limited = ref(true)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

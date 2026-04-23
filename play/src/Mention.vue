<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Mention Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-mention
        data-testid="mention-basic"
        v-model="basicValue"
        :options="users"
        type="textarea"
        placeholder="Type @ to mention someone"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Type @ and pick)</h3>
      <el-mention
        data-testid="mention-interact"
        v-model="pickedValue"
        :options="users"
        type="textarea"
        placeholder="Mention a user"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (loading toggle)</h3>
      <el-button data-testid="mention-toggle-loading" @click="loading = !loading">
        Toggle loading: <span data-testid="state-indicator">{{ loading ? 'loading' : 'ready' }}</span>
      </el-button>
      <el-mention
        data-testid="mention-state-target"
        v-model="stateValue"
        :options="users"
        :loading="loading"
        type="textarea"
        placeholder="State-variant"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const users = [
  { value: 'alice', label: 'Alice' },
  { value: 'bob', label: 'Bob' },
  { value: 'carol', label: 'Carol' },
  { value: 'dave', label: 'Dave' },
  { value: 'eve', label: 'Eve' },
]

const basicValue = ref('')
const pickedValue = ref('')
const stateValue = ref('')
const loading = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

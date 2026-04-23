<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Switch Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-switch
        data-testid="switch-basic"
        v-model="basicValue"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (toggle on/off)</h3>
      <el-switch
        data-testid="switch-interact"
        v-model="pickedValue"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue ? 'on' : 'off' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (loading toggle)</h3>
      <el-button data-testid="switch-toggle-loading" @click="loading = !loading">
        Toggle loading: <span data-testid="state-indicator">{{ loading ? 'loading' : 'idle' }}</span>
      </el-button>
      <el-switch
        data-testid="switch-state-target"
        v-model="stateValue"
        :loading="loading"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref(false)
const pickedValue = ref(false)
const stateValue = ref(true)
const loading = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

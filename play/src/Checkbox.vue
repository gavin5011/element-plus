<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Checkbox Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-checkbox-group data-testid="checkbox-basic" v-model="basicValue">
        <el-checkbox value="Apple" label="Apple" />
        <el-checkbox value="Banana" label="Banana" />
        <el-checkbox value="Cherry" label="Cherry" />
      </el-checkbox-group>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (check/uncheck)</h3>
      <el-checkbox-group data-testid="checkbox-interact" v-model="pickedValue">
        <el-checkbox value="Apple" label="Apple" />
        <el-checkbox value="Banana" label="Banana" />
        <el-checkbox value="Cherry" label="Cherry" />
      </el-checkbox-group>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue.join(', ') || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (disabled toggle)</h3>
      <el-button data-testid="checkbox-toggle-disabled" @click="disabled = !disabled">
        Toggle disabled: <span data-testid="state-indicator">{{ disabled ? 'disabled' : 'enabled' }}</span>
      </el-button>
      <el-checkbox-group data-testid="checkbox-state-target" v-model="stateValue" :disabled="disabled">
        <el-checkbox value="Apple" label="Apple" />
        <el-checkbox value="Banana" label="Banana" />
        <el-checkbox value="Cherry" label="Cherry" />
      </el-checkbox-group>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref<string[]>([])
const pickedValue = ref<string[]>([])
const stateValue = ref<string[]>(['Apple'])
const disabled = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">ColorPicker Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-color-picker
        data-testid="color-picker-basic"
        v-model="basicValue"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (pick color)</h3>
      <el-color-picker
        data-testid="color-picker-interact"
        v-model="pickedValue"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (alpha slider toggle)</h3>
      <el-button data-testid="color-picker-toggle-alpha" @click="showAlpha = !showAlpha">
        Toggle alpha: <span data-testid="state-indicator">{{ showAlpha ? 'alpha on' : 'alpha off' }}</span>
      </el-button>
      <el-color-picker
        data-testid="color-picker-state-target"
        v-model="stateValue"
        :show-alpha="showAlpha"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref('#409EFF')
const pickedValue = ref('')
const stateValue = ref('#67C23A')
const showAlpha = ref(false)
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

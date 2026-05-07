<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Radio Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-radio-group data-testid="radio-basic" v-model="basicValue">
        <el-radio value="Small" label="Small">Small</el-radio>
        <el-radio value="Medium" label="Medium">Medium</el-radio>
        <el-radio value="Large" label="Large">Large</el-radio>
      </el-radio-group>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (pick one)</h3>
      <el-radio-group data-testid="radio-interact" v-model="pickedValue">
        <el-radio value="Small" label="Small">Small</el-radio>
        <el-radio value="Medium" label="Medium">Medium</el-radio>
        <el-radio value="Large" label="Large">Large</el-radio>
      </el-radio-group>
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (button mode toggle)</h3>
      <el-button
        data-testid="radio-toggle-button"
        @click="buttonMode = !buttonMode"
      >
        Toggle mode:
        <span data-testid="state-indicator">{{
          buttonMode ? 'button' : 'default'
        }}</span>
      </el-button>
      <el-radio-group
        v-if="!buttonMode"
        data-testid="radio-state-target"
        v-model="stateValue"
      >
        <el-radio value="Small" label="Small">Small</el-radio>
        <el-radio value="Medium" label="Medium">Medium</el-radio>
        <el-radio value="Large" label="Large">Large</el-radio>
      </el-radio-group>
      <el-radio-group
        v-else
        data-testid="radio-state-target"
        v-model="stateValue"
      >
        <el-radio-button value="Small" label="Small">Small</el-radio-button>
        <el-radio-button value="Medium" label="Medium">Medium</el-radio-button>
        <el-radio-button value="Large" label="Large">Large</el-radio-button>
      </el-radio-group>
    </section>

    <section data-testid="scenario-cat1-radio-selection">
      <h3>S5: cat1 fixture - Radio group selection mismatch</h3>
      <p>Click "B": handler always sets to "A".</p>
      <el-button data-testid="cat1-radio-option-b" @click="cat1RadioSetB"
        >Click B</el-button
      >
      <span
        >Selected:
        <span data-testid="cat1-radio-selected">{{
          cat1RadioValue
        }}</span></span
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref('Medium')
const pickedValue = ref('')
const stateValue = ref('Medium')
const buttonMode = ref(false)

const cat1RadioValue = ref('A')
function cat1RadioSetB() {
  // Bug: should set to 'B' but always sets to 'A'
  cat1RadioValue.value = 'A'
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

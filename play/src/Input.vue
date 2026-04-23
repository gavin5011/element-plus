<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Input Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-input
        data-testid="input-basic"
        v-model="textA"
        placeholder="Type something"
        clearable
        style="width: 240px"
      />
      <el-input
        data-testid="input-password"
        v-model="textB"
        type="password"
        placeholder="Password"
        show-password
        style="width: 240px"
      />
      <el-input
        data-testid="input-disabled"
        model-value="Disabled"
        disabled
        style="width: 240px"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Typing + Echo)</h3>
      <el-input
        data-testid="input-echo"
        v-model="echoText"
        placeholder="Type and I echo"
        maxlength="30"
        show-word-limit
        style="width: 300px"
      />
      <div data-testid="echo-value">Value: "{{ echoText }}"</div>
      <div data-testid="echo-length">Length: {{ echoText.length }}</div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (size cycle)</h3>
      <el-button data-testid="input-cycle-size" @click="cycleInputSize">
        Cycle size: <span data-testid="state-indicator">{{ currentInputSize }}</span>
      </el-button>
      <el-input
        :size="currentInputSize"
        v-model="textState"
        placeholder="State-variant"
        style="width: 280px"
        data-testid="input-state-target"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const textA = ref('')
const textB = ref('')
const echoText = ref('')
const textState = ref('')

const sizes = ['large', 'default', 'small'] as const
type Size = typeof sizes[number]
const currentInputSize = ref<Size>('default')
function cycleInputSize() {
  const i = sizes.indexOf(currentInputSize.value)
  currentInputSize.value = sizes[(i + 1) % sizes.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Button Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-button data-testid="btn-default">Default</el-button>
      <el-button type="primary" data-testid="btn-primary">Primary</el-button>
      <el-button type="success" data-testid="btn-success">Success</el-button>
      <el-button type="warning" data-testid="btn-warning">Warning</el-button>
      <el-button type="danger" data-testid="btn-danger" disabled>Disabled</el-button>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click Counter)</h3>
      <el-button data-testid="btn-counter" type="primary" @click="count++">
        Clicked <span data-testid="counter-value">{{ count }}</span> times
      </el-button>
      <el-button data-testid="btn-reset" @click="count = 0">Reset</el-button>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (size cycle)</h3>
      <el-button data-testid="btn-cycle-size" @click="cycleSize">
        Cycle size: <span data-testid="state-indicator">{{ currentSize }}</span>
      </el-button>
      <el-button :size="currentSize" type="primary" data-testid="btn-state-target">
        Target
      </el-button>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const count = ref(0)

const sizes = ['large', 'default', 'small'] as const
type Size = typeof sizes[number]
const currentSize = ref<Size>('default')
function cycleSize() {
  const i = sizes.indexOf(currentSize.value)
  currentSize.value = sizes[(i + 1) % sizes.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; }
section h3 { margin-bottom: 8px; color: #606266; }
</style>

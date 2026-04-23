<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Badge Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-badge :value="12" data-testid="badge-numeric">
        <el-button>Messages</el-button>
      </el-badge>
      <el-badge :value="3" type="primary" data-testid="badge-primary">
        <el-button>Replies</el-button>
      </el-badge>
      <el-badge value="hot" type="danger" data-testid="badge-text">
        <el-button>Trending</el-button>
      </el-badge>
      <el-badge is-dot data-testid="badge-dot">
        <el-button>Notify</el-button>
      </el-badge>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Increment Badge Count)</h3>
      <el-badge :value="count" data-testid="badge-counter" :max="99">
        <el-button data-testid="btn-increment" @click="count++">Add Message</el-button>
      </el-badge>
      <el-button data-testid="btn-reset-badge" @click="count = 0">Reset</el-button>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (value cycle — exercises max overflow)</h3>
      <el-button data-testid="badge-cycle-value" @click="cycleBadgeValue">
        Cycle value: <span data-testid="state-indicator">{{ stateValue }}</span>
      </el-button>
      <el-badge :value="stateValue" :max="99" data-testid="badge-state-target">
        <el-button>Messages</el-button>
      </el-badge>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const count = ref(5)

const values = [0, 5, 150] as const
const stateValue = ref<number>(0)
function cycleBadgeValue() {
  const i = values.indexOf(stateValue.value as any)
  stateValue.value = values[(i + 1) % values.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 24px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

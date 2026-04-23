<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">InfiniteScroll Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <div
        data-testid="infinitescroll-basic"
        class="scroll-box"
        v-infinite-scroll="noop"
      >
        <div v-for="n in basicItems" :key="n" class="row">Item {{ n }}</div>
      </div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (scroll to load)</h3>
      <div
        data-testid="infinitescroll-interact"
        class="scroll-box"
        v-infinite-scroll="loadMoreInteract"
        :infinite-scroll-distance="10"
        :infinite-scroll-immediate="false"
      >
        <div v-for="n in interactItems" :key="n" class="row">Item {{ n }}</div>
      </div>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ interactItems.length }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (disabled toggle)</h3>
      <el-button data-testid="infinitescroll-toggle-disabled" @click="disabled = !disabled">
        Toggle loading: <span data-testid="state-indicator">{{ disabled ? 'disabled' : 'enabled' }}</span>
      </el-button>
      <div
        data-testid="infinitescroll-state-target"
        class="scroll-box"
        v-infinite-scroll="loadMoreState"
        :infinite-scroll-disabled="disabled"
        :infinite-scroll-immediate="false"
      >
        <div v-for="n in stateItems" :key="n" class="row">Item {{ n }}</div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicItems = ref(Array.from({ length: 20 }, (_, i) => i + 1))
const interactItems = ref(Array.from({ length: 20 }, (_, i) => i + 1))
const stateItems = ref(Array.from({ length: 20 }, (_, i) => i + 1))
const disabled = ref(false)

function noop() {}

function loadMoreInteract() {
  const len = interactItems.value.length
  for (let i = 1; i <= 5; i++) interactItems.value.push(len + i)
}

function loadMoreState() {
  const len = stateItems.value.length
  for (let i = 1; i <= 5; i++) stateItems.value.push(len + i)
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.scroll-box { width: 300px; height: 200px; overflow: auto; border: 1px solid #dcdfe6; padding: 8px; }
.row { padding: 6px 4px; border-bottom: 1px solid #f0f0f0; }
</style>

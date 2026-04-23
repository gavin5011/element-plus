<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tabs Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tabs data-testid="tabs-basic" v-model="basicValue">
        <el-tab-pane label="Overview" name="overview">Overview content</el-tab-pane>
        <el-tab-pane label="Details" name="details">Details content</el-tab-pane>
        <el-tab-pane label="Reviews" name="reviews">Reviews content</el-tab-pane>
        <el-tab-pane label="FAQ" name="faq">FAQ content</el-tab-pane>
      </el-tabs>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click tab)</h3>
      <el-tabs data-testid="tabs-interact" v-model="pickedValue" @tab-change="onTabChange">
        <el-tab-pane label="Overview" name="overview">Overview content</el-tab-pane>
        <el-tab-pane label="Details" name="details">Details content</el-tab-pane>
        <el-tab-pane label="Reviews" name="reviews">Reviews content</el-tab-pane>
        <el-tab-pane label="FAQ" name="faq">FAQ content</el-tab-pane>
      </el-tabs>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (card/border toggle)</h3>
      <el-button data-testid="tabs-toggle-card" @click="toggleStyle">
        Toggle style: <span data-testid="state-indicator">{{ tabStyle }}</span>
      </el-button>
      <el-tabs
        data-testid="tabs-state-target"
        v-model="stateValue"
        :type="tabStyle"
      >
        <el-tab-pane label="Overview" name="overview">Overview content</el-tab-pane>
        <el-tab-pane label="Details" name="details">Details content</el-tab-pane>
        <el-tab-pane label="Reviews" name="reviews">Reviews content</el-tab-pane>
        <el-tab-pane label="FAQ" name="faq">FAQ content</el-tab-pane>
      </el-tabs>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref('overview')
const pickedValue = ref('overview')
const stateValue = ref('overview')
const tabStyle = ref<'card' | 'border-card'>('card')

function onTabChange(name: string | number) {
  pickedValue.value = String(name)
}

function toggleStyle() {
  tabStyle.value = tabStyle.value === 'card' ? 'border-card' : 'card'
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

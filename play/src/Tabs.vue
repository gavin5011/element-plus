<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tabs Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tabs data-testid="tabs-basic" v-model="basicValue">
        <el-tab-pane label="Overview" name="overview"
          >Overview content</el-tab-pane
        >
        <el-tab-pane label="Details" name="details"
          >Details content</el-tab-pane
        >
        <el-tab-pane label="Reviews" name="reviews"
          >Reviews content</el-tab-pane
        >
        <el-tab-pane label="FAQ" name="faq">FAQ content</el-tab-pane>
      </el-tabs>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click tab)</h3>
      <el-tabs
        data-testid="tabs-interact"
        v-model="pickedValue"
        @tab-change="onTabChange"
      >
        <el-tab-pane label="Overview" name="overview"
          >Overview content</el-tab-pane
        >
        <el-tab-pane label="Details" name="details"
          >Details content</el-tab-pane
        >
        <el-tab-pane label="Reviews" name="reviews"
          >Reviews content</el-tab-pane
        >
        <el-tab-pane label="FAQ" name="faq">FAQ content</el-tab-pane>
      </el-tabs>
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
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
        <el-tab-pane label="Overview" name="overview"
          >Overview content</el-tab-pane
        >
        <el-tab-pane label="Details" name="details"
          >Details content</el-tab-pane
        >
        <el-tab-pane label="Reviews" name="reviews"
          >Reviews content</el-tab-pane
        >
        <el-tab-pane label="FAQ" name="faq">FAQ content</el-tab-pane>
      </el-tabs>
    </section>

    <section data-testid="scenario-cat4-testid-rename">
      <h3>
        S4: cat4 fixture — Tabs testid rename drift (post-freeze refactor)
      </h3>
      <p>
        Spec was frozen with selector `data-testid="tab-pane-detail"`. UI
        refactor renamed the testid to `data-testid="tab-pane-details"`. Spec
        selector now fails to resolve.
      </p>
      <el-tabs data-testid="tabs-renamed-target" v-model="renamedValue">
        <el-tab-pane
          data-testid="tab-trigger-overview"
          label="Overview"
          name="overview"
        >
          Overview content
        </el-tab-pane>
        <!-- testid was tab-pane-detail (frozen spec); refactored to tab-pane-details -->
        <el-tab-pane
          data-testid="tab-trigger-detail"
          label="Detail"
          name="detail"
        >
          <span data-testid="tab-pane-details"
            >Detail content (renamed testid: was tab-pane-detail)</span
          >
        </el-tab-pane>
      </el-tabs>
    </section>

    <section data-testid="scenario-cat3-tabs-gap-shift">
      <h3>cat3 fixture - Tabs gap shift breaks position coupling</h3>
      <p>
        Visual mutation creates overlay/clip; functional click
        intercepted/clipped.
      </p>
      <div style="position: relative; display: inline-block">
        <el-button data-testid="cat3-tabs-gap-shift-button"
          >Tab button</el-button
        >
        <div
          style="
            position: absolute;
            inset: 0;
            background: rgba(0, 0, 255, 0.05);
            pointer-events: auto;
            z-index: 10;
          "
        ></div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref('overview')
const pickedValue = ref('overview')
const stateValue = ref('overview')
const tabStyle = ref<'card' | 'border-card'>('card')
const renamedValue = ref('overview')

function onTabChange(name: string | number) {
  pickedValue.value = String(name)
}

function toggleStyle() {
  tabStyle.value = tabStyle.value === 'card' ? 'border-card' : 'card'
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

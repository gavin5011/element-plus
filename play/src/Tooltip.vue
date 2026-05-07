<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tooltip Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tooltip content="Basic tooltip content" placement="top">
        <el-button data-testid="tooltip-basic">Hover me</el-button>
      </el-tooltip>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (hover to show)</h3>
      <el-tooltip
        content="Interact tooltip"
        placement="top"
        :show-after="1000"
        :hide-after="0"
        @show="onShow"
        @hide="onHide"
      >
        <el-button data-testid="tooltip-interact">Hover for interact</el-button>
      </el-tooltip>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (trigger toggle)</h3>
      <el-button data-testid="tooltip-toggle-trigger" @click="toggleTrigger">
        Toggle trigger: <span data-testid="state-indicator">{{ trigger }}</span>
      </el-button>
      <el-tooltip
        :content="`Trigger=${trigger}`"
        :trigger="trigger"
        placement="top"
      >
        <el-button data-testid="tooltip-state-target">Target</el-button>
      </el-tooltip>
    </section>

    <section data-testid="scenario-cat6-tooltip-hover-delay">
      <h3>S4: cat6 fixture - 200ms hover delay (race vs same-session retry)</h3>
      <el-button
        data-testid="tooltip-hover-trigger"
        @mouseenter="hoverDelayHandler"
        >Hover (200ms delay)</el-button
      >
      <span v-if="hoverDelayShown" data-testid="tooltip-hover-content"
        >Tooltip after 200ms</span
      >
    </section>

    <section data-testid="scenario-cat6-tooltip-hide-delay">
      <h3>S5: cat6 fixture - 150ms hide delay (race vs same-session retry)</h3>
      <el-button
        data-testid="tooltip-hide-trigger"
        @mouseenter="hideDelayHandler"
        @mouseleave="hideDelayHide"
        >Hover then unhover (150ms hide)</el-button
      >
      <span v-if="hideDelayShown" data-testid="tooltip-hide-content"
        >Visible until hide delay completes</span
      >
    </section>

    <section data-testid="scenario-cat6-tooltip-async-content">
      <h3>
        S6: cat6 fixture - Async content load 250ms (race vs same-session retry)
      </h3>
      <el-button
        data-testid="tooltip-async-trigger"
        @click="asyncContentHandler"
        >Click (250ms async)</el-button
      >
      <span v-if="asyncContentShown" data-testid="tooltip-async-content"
        >Async content loaded</span
      >
    </section>

    <section data-testid="scenario-cat3-tooltip-zindex">
      <h3>cat3 fixture - Tooltip z-index overlap coupling</h3>
      <p>
        Visual mutation creates overlay/clip; functional click
        intercepted/clipped.
      </p>
      <div style="position: relative; display: inline-block">
        <el-button data-testid="cat3-tooltip-zindex-trigger">Trigger</el-button>
        <div
          style="
            position: absolute;
            inset: 0;
            background: rgba(255, 0, 255, 0.05);
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

const pickedValue = ref('(none)')
const trigger = ref<'hover' | 'click'>('hover')

function onShow() {
  pickedValue.value = 'shown'
}
function onHide() {
  pickedValue.value = 'hidden'
}
function toggleTrigger() {
  trigger.value = trigger.value === 'hover' ? 'click' : 'hover'
}

// cat6 fixtures
const hoverDelayShown = ref(false)
function hoverDelayHandler() {
  setTimeout(() => {
    hoverDelayShown.value = true
  }, 200)
}

const hideDelayShown = ref(false)
let hideTimer: ReturnType<typeof setTimeout> | null = null
function hideDelayHandler() {
  if (hideTimer) clearTimeout(hideTimer)
  hideDelayShown.value = true
}
function hideDelayHide() {
  hideTimer = setTimeout(() => {
    hideDelayShown.value = false
  }, 150)
}

const asyncContentShown = ref(false)
function asyncContentHandler() {
  setTimeout(() => {
    asyncContentShown.value = true
  }, 250)
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

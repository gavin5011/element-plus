<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Popover Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-popover
        title="Basic Popover"
        content="Basic popover text content"
        placement="top"
        :width="240"
      >
        <template #reference>
          <el-button data-testid="popover-basic">Basic</el-button>
        </template>
      </el-popover>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (show / hide)</h3>
      <el-popover
        title="Interact Popover"
        placement="top"
        :width="240"
        @show="onShow"
        @hide="onHide"
      >
        <template #default>
          <div>Popover content body</div>
        </template>
        <template #reference>
          <el-button data-testid="popover-interact">Interact</el-button>
        </template>
      </el-popover>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (placement cycle)</h3>
      <el-button data-testid="popover-toggle-placement" @click="cyclePlacement">
        Toggle placement:
        <span data-testid="state-indicator">{{ placement }}</span>
      </el-button>
      <el-popover
        :title="`Placement ${placement}`"
        content="Cycled placement content"
        :placement="placement"
        :width="240"
      >
        <template #reference>
          <el-button data-testid="popover-state-target">Target</el-button>
        </template>
      </el-popover>
    </section>

    <section data-testid="scenario-cat3-overlay-pointer-events">
      <h3>
        S4: cat3 fixture — Popover overlay pointer-events:none coupling
        (visual+functional)
      </h3>
      <p>
        Mutation: an invisible overlay wrapper around the trigger has
        `pointer-events: none` (visual change). When user clicks the trigger,
        the click is intercepted by the overlay wrapping logic and never reaches
        the trigger → popover never opens (functional symptom). Coupling: visual
        change → functional symptom via causal link.
      </p>
      <div class="cat3-overlay-wrapper" data-testid="cat3-overlay-wrapper">
        <el-popover
          title="Coupling Popover"
          content="Coupling popover body content"
          placement="top"
          :width="240"
        >
          <template #reference>
            <el-button data-testid="cat3-popover-trigger"
              >Click to open</el-button
            >
          </template>
          <template #default>
            <div data-testid="cat3-popover-content">
              Popover content visible after click
            </div>
          </template>
        </el-popover>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pickedValue = ref('(none)')
const placements = ['top', 'bottom', 'left', 'right'] as const
type Placement = (typeof placements)[number]
const placement = ref<Placement>('top')

function onShow() {
  pickedValue.value = 'shown'
}
function onHide() {
  pickedValue.value = 'hidden'
}
function cyclePlacement() {
  const idx = placements.indexOf(placement.value)
  placement.value = placements[(idx + 1) % placements.length]
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
/* cat3 mutation: pointer-events:none on overlay wrapper. Visible (no opacity change),
   but intercepts pointer events to children including the trigger button. */
.cat3-overlay-wrapper {
  position: relative;
  pointer-events: none;
}
.cat3-overlay-wrapper * {
  pointer-events: none;
}
</style>

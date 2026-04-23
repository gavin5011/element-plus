<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Popover Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-popover title="Basic Popover" content="Basic popover text content" placement="top" :width="240">
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
        Toggle placement: <span data-testid="state-indicator">{{ placement }}</span>
      </el-button>
      <el-popover :title="`Placement ${placement}`" content="Cycled placement content" :placement="placement" :width="240">
        <template #reference>
          <el-button data-testid="popover-state-target">Target</el-button>
        </template>
      </el-popover>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pickedValue = ref('(none)')
const placements = ['top', 'bottom', 'left', 'right'] as const
type Placement = typeof placements[number]
const placement = ref<Placement>('top')

function onShow() { pickedValue.value = 'shown' }
function onHide() { pickedValue.value = 'hidden' }
function cyclePlacement() {
  const idx = placements.indexOf(placement.value)
  placement.value = placements[(idx + 1) % placements.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

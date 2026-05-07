<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Timeline Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-timeline data-testid="timeline-basic"
        ><el-timeline-item timestamp="2024-01-01">A</el-timeline-item
        ><el-timeline-item timestamp="2024-01-02"
          >B</el-timeline-item
        ></el-timeline
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button data-testid="timeline-add-item" @click="tlCount++"
        >Add</el-button
      ><el-timeline data-testid="timeline-interact"
        ><el-timeline-item
          v-for="i in tlCount"
          :key="i"
          :timestamp="`Item ${i}`"
          >{{ i }}</el-timeline-item
        ></el-timeline
      >
      <div data-testid="picked-value-display">
        Count: <span data-testid="picked-value">{{ tlCount }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="timeline-cycle-placement"
        @click="tlPlacement = tlPlacement === 'top' ? 'bottom' : 'top'"
        >Place:
        <span data-testid="state-indicator">{{ tlPlacement }}</span></el-button
      ><el-timeline data-testid="timeline-state-target"
        ><el-timeline-item :placement="tlPlacement" timestamp="ts"
          >item</el-timeline-item
        ></el-timeline
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const tlCount = ref(2)
const tlPlacement = ref('top')
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

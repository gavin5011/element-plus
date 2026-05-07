<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Segmented Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-segmented
        v-model="segValue"
        :options="['A', 'B', 'C']"
        data-testid="segmented-basic"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button data-testid="segmented-set-b" @click="segValue = 'B'"
        >Set B</el-button
      ><el-segmented
        v-model="segValue"
        :options="['A', 'B', 'C']"
        data-testid="segmented-interact"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ segValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="segmented-toggle-disabled"
        @click="segDisabled = !segDisabled"
        >Disabled:
        <span data-testid="state-indicator">{{
          segDisabled ? 'on' : 'off'
        }}</span></el-button
      ><el-segmented
        v-model="segValue"
        :options="['A', 'B']"
        :disabled="segDisabled"
        data-testid="segmented-state-target"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const segValue = ref('A')
const segDisabled = ref(false)
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

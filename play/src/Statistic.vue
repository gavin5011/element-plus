<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Statistic Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-statistic
        title="Daily"
        :value="statValue"
        data-testid="statistic-basic"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button data-testid="statistic-increment" @click="statValue += 100"
        >+100</el-button
      ><el-statistic
        title="Counter"
        :value="statValue"
        data-testid="statistic-interact"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ statValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="statistic-cycle-precision"
        @click="statPrec = statPrec === 0 ? 2 : 0"
        >Prec:
        <span data-testid="state-indicator">{{ statPrec }}</span></el-button
      ><el-statistic
        :value="3.14159"
        :precision="statPrec"
        data-testid="statistic-state-target"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const statValue = ref(1234)
const statPrec = ref(0)
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

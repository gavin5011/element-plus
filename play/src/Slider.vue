<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Slider Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-slider
        data-testid="slider-basic"
        v-model="basicValue"
        :min="0"
        :max="100"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (drag to change)</h3>
      <el-slider
        data-testid="slider-interact"
        v-model="pickedValue"
        :min="0"
        :max="100"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (range/single toggle)</h3>
      <el-button data-testid="slider-toggle-range" @click="toggleRange">
        Toggle mode:
        <span data-testid="state-indicator">{{
          rangeMode ? 'range' : 'single'
        }}</span>
      </el-button>
      <el-slider
        v-if="!rangeMode"
        data-testid="slider-state-target"
        v-model="stateSingle"
        :min="0"
        :max="100"
      />
      <el-slider
        v-else
        data-testid="slider-state-target"
        v-model="stateRange"
        :min="0"
        :max="100"
        range
      />
    </section>

    <section data-testid="scenario-cat1-slider-clamp">
      <h3>S5: cat1 fixture - Slider clamp inversion</h3>
      <p>Click "Set 50": handler clamps to max instead.</p>
      <el-button data-testid="cat1-slider-set-50" @click="cat1SliderSet50"
        >Set 50</el-button
      >
      <span
        >Value:
        <span data-testid="cat1-slider-value">{{ cat1SliderValue }}</span></span
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicValue = ref(30)
const pickedValue = ref(50)
const stateSingle = ref(40)
const stateRange = ref<[number, number]>([20, 70])
const rangeMode = ref(false)

const toggleRange = () => {
  rangeMode.value = !rangeMode.value
}

const cat1SliderValue = ref(0)
function cat1SliderSet50() {
  // Bug: should set to 50 but inverted clamp pushes to 100 (max)
  cat1SliderValue.value = 100
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

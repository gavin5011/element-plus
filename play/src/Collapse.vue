<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Collapse Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-collapse data-testid="collapse-basic" v-model="basicActive" style="width: 400px">
        <el-collapse-item title="Shipping" name="shipping">
          <p>Orders ship within 2 business days of payment confirmation.</p>
        </el-collapse-item>
        <el-collapse-item title="Returns" name="returns">
          <p>Return requests accepted within 30 days of delivery.</p>
        </el-collapse-item>
        <el-collapse-item title="Warranty" name="warranty">
          <p>Two-year limited warranty covers manufacturing defects.</p>
        </el-collapse-item>
      </el-collapse>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (expand panel)</h3>
      <el-collapse
        data-testid="collapse-interact"
        v-model="pickedActive"
        style="width: 400px"
        @change="onChange"
      >
        <el-collapse-item title="Shipping" name="shipping">
          <p>Orders ship within 2 business days of payment confirmation.</p>
        </el-collapse-item>
        <el-collapse-item title="Returns" name="returns">
          <p>Return requests accepted within 30 days of delivery.</p>
        </el-collapse-item>
        <el-collapse-item title="Warranty" name="warranty">
          <p>Two-year limited warranty covers manufacturing defects.</p>
        </el-collapse-item>
      </el-collapse>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ Array.isArray(pickedActive) ? pickedActive.join(',') : pickedActive || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (accordion toggle)</h3>
      <el-button data-testid="collapse-toggle-accordion" @click="accordion = !accordion">
        Toggle accordion: <span data-testid="state-indicator">{{ accordion ? 'accordion' : 'multiple' }}</span>
      </el-button>
      <el-collapse
        data-testid="collapse-state-target"
        v-model="stateActive"
        :accordion="accordion"
        style="width: 400px"
      >
        <el-collapse-item title="Shipping" name="shipping">
          <p>Orders ship within 2 business days of payment confirmation.</p>
        </el-collapse-item>
        <el-collapse-item title="Returns" name="returns">
          <p>Return requests accepted within 30 days of delivery.</p>
        </el-collapse-item>
        <el-collapse-item title="Warranty" name="warranty">
          <p>Two-year limited warranty covers manufacturing defects.</p>
        </el-collapse-item>
      </el-collapse>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicActive = ref<string[]>([])
const pickedActive = ref<string[] | string>([])
const accordion = ref(false)
const stateActive = ref<string[] | string>([])

function onChange(val: string[] | string) {
  pickedActive.value = val
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Affix Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-affix data-testid="affix-basic" :offset="80">
        <el-button type="primary">Affixed (offset 80)</el-button>
      </el-affix>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (scroll triggers affix)</h3>
      <el-affix
        data-testid="affix-interact"
        :offset="80"
        @change="onChange"
      >
        <el-button type="primary">Scroll to stick</el-button>
      </el-affix>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ fixed ? 'fixed' : 'unfixed' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (offset position)</h3>
      <el-button data-testid="affix-toggle-position" @click="bottomMode = !bottomMode">
        Toggle position: <span data-testid="state-indicator">{{ bottomMode ? 'bottom' : 'top' }}</span>
      </el-button>
      <el-affix
        data-testid="affix-state-target"
        :offset="60"
        :position="bottomMode ? 'bottom' : 'top'"
      >
        <el-button>State-variant button</el-button>
      </el-affix>
    </section>

    <div class="spacer">Scroll padding (placeholder content to enable scrolling)</div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const fixed = ref(false)
const bottomMode = ref(false)

function onChange(isFixed: boolean) {
  fixed.value = isFixed
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; min-height: 1600px; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.spacer { margin-top: 400px; color: #909399; }
</style>

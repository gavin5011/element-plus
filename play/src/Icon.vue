<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Icon Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-icon data-testid="icon-check" color="#409EFC" :size="20"><el-icon-check /></el-icon>
      <el-icon data-testid="icon-menu" :size="20"><el-icon-menu /></el-icon>
      <el-icon data-testid="icon-search" color="red" :size="30"><el-icon-search /></el-icon>
      <el-icon data-testid="icon-edit" :size="40"><el-icon-edit /></el-icon>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Toggle Visibility)</h3>
      <el-button data-testid="toggle-btn" @click="visible = !visible">
        Toggle Icon ({{ visible ? 'hide' : 'show' }})
      </el-button>
      <el-icon v-if="visible" data-testid="icon-star" color="gold" :size="32">
        <el-icon-star-filled />
      </el-icon>
      <span v-else data-testid="icon-hidden">(hidden)</span>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (color cycle)</h3>
      <el-button data-testid="icon-cycle-color" @click="cycleColor">
        Cycle color: <span data-testid="state-indicator">{{ currentColor }}</span>
      </el-button>
      <el-icon :color="currentColor" :size="40" data-testid="icon-state-target">
        <el-icon-star-filled />
      </el-icon>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const visible = ref(true)

const colors = ['#409EFC', '#F56C6C', '#E6A23C'] as const
type Color = typeof colors[number]
const currentColor = ref<Color>('#409EFC')
function cycleColor() {
  const i = colors.indexOf(currentColor.value)
  currentColor.value = colors[(i + 1) % colors.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 12px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

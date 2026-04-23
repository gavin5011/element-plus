<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Avatar Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-avatar data-testid="avatar-default" :size="50">
        User
      </el-avatar>
      <el-avatar data-testid="avatar-square" shape="square" :size="50">
        A
      </el-avatar>
      <el-avatar data-testid="avatar-large" :size="80" :src="avatarUrl" />
      <el-avatar data-testid="avatar-small" :size="32">
        B
      </el-avatar>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Change Avatar Source)</h3>
      <el-avatar data-testid="avatar-dynamic" :size="60" :src="currentSrc">
        ?
      </el-avatar>
      <el-button data-testid="btn-swap-avatar" @click="toggle">
        Current: <span data-testid="current-label">{{ label }}</span>
      </el-button>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (shape cycle)</h3>
      <el-button data-testid="avatar-cycle-shape" @click="cycleShape">
        Cycle shape: <span data-testid="state-indicator">{{ currentShape }}</span>
      </el-button>
      <el-avatar :shape="currentShape" :size="60" data-testid="avatar-state-target">
        S
      </el-avatar>
    </section>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

const avatarUrl = 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png'
const broken = 'https://not-an-image.invalid/x.png'

const idx = ref(0)
const currentSrc = computed(() => (idx.value % 2 === 0 ? avatarUrl : broken))
const label = computed(() => (idx.value % 2 === 0 ? 'valid' : 'broken'))
function toggle() { idx.value++ }

const shapes = ['circle', 'square'] as const
type Shape = typeof shapes[number]
const currentShape = ref<Shape>('circle')
function cycleShape() {
  const i = shapes.indexOf(currentShape.value)
  currentShape.value = shapes[(i + 1) % shapes.length]
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 20px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">ImageViewer Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-button data-testid="imageviewer-basic" @click="basicOpen = true">Open viewer</el-button>
      <el-image-viewer
        v-if="basicOpen"
        :url-list="images"
        @close="basicOpen = false"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (open → close)</h3>
      <el-button data-testid="imageviewer-interact" @click="openInteract">Open viewer</el-button>
      <el-image-viewer
        v-if="interactOpen"
        :url-list="images"
        @close="closeInteract"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ interactState }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (zoom rate)</h3>
      <el-button data-testid="imageviewer-toggle-zoomrate" @click="highZoom = !highZoom">
        Toggle zoom rate: <span data-testid="state-indicator">{{ highZoom ? 'rate-2' : 'rate-1.2' }}</span>
      </el-button>
      <el-button data-testid="imageviewer-state-target" @click="stateOpen = true">Open viewer</el-button>
      <el-image-viewer
        v-if="stateOpen"
        :url-list="images"
        :zoom-rate="highZoom ? 2 : 1.2"
        @close="stateOpen = false"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const images = [
  'https://fastly.jsdelivr.net/npm/@vant/assets/cat.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/leaf.jpeg',
  'https://fastly.jsdelivr.net/npm/@vant/assets/apple-1.jpeg',
]

const basicOpen = ref(false)
const interactOpen = ref(false)
const interactState = ref('closed')
const highZoom = ref(false)
const stateOpen = ref(false)

function openInteract() {
  interactOpen.value = true
  interactState.value = 'open'
}
function closeInteract() {
  interactOpen.value = false
  interactState.value = 'closed'
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

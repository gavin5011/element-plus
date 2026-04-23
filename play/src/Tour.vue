<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tour Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-button data-testid="tour-basic" ref="target1Ref" @click="basicOpen = true">Start Basic Tour</el-button>
      <el-button ref="target2Ref">Step 2 Target</el-button>
      <el-button ref="target3Ref">Step 3 Target</el-button>
    </section>

    <el-tour v-model="basicOpen" data-testid="tour-basic-root">
      <el-tour-step :target="target1Ref?.$el" title="Step 1" description="First step" />
      <el-tour-step :target="target2Ref?.$el" title="Step 2" description="Second step" />
      <el-tour-step :target="target3Ref?.$el" title="Step 3" description="Third step" />
    </el-tour>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (open / step change)</h3>
      <el-button data-testid="tour-interact" ref="t1Ref" @click="openInteract">Open Interact Tour</el-button>
      <el-button ref="t2Ref">Target B</el-button>
      <el-button ref="t3Ref">Target C</el-button>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">step={{ pickedValue }}</span>
      </div>
    </section>

    <el-tour data-testid="tour-interact-root" v-model="interactOpen" @change="onChange" @close="onClose">
      <el-tour-step :target="t1Ref?.$el" title="A" description="Step A" />
      <el-tour-step :target="t2Ref?.$el" title="B" description="Step B" />
      <el-tour-step :target="t3Ref?.$el" title="C" description="Step C" />
    </el-tour>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (arrow toggle)</h3>
      <el-button data-testid="tour-toggle-arrow" @click="showArrow = !showArrow">
        Toggle arrow: <span data-testid="state-indicator">{{ showArrow ? 'show' : 'hide' }}</span>
      </el-button>
      <el-button data-testid="tour-state-target" ref="sRef" @click="stateOpen = true">Open state tour</el-button>
    </section>

    <el-tour data-testid="tour-state-root" v-model="stateOpen" :show-arrow="showArrow">
      <el-tour-step :target="sRef?.$el" title="State" description="Arrow visibility variant" />
    </el-tour>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const basicOpen = ref(false)
const interactOpen = ref(false)
const stateOpen = ref(false)
const showArrow = ref(true)
const pickedValue = ref(0)

const target1Ref = ref<any>(null)
const target2Ref = ref<any>(null)
const target3Ref = ref<any>(null)
const t1Ref = ref<any>(null)
const t2Ref = ref<any>(null)
const t3Ref = ref<any>(null)
const sRef = ref<any>(null)

function openInteract() {
  interactOpen.value = true
  pickedValue.value = 0
}
function onChange(idx: number) { pickedValue.value = idx }
function onClose() { pickedValue.value = -1 }
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

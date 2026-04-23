<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Popconfirm Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-popconfirm title="Delete this record?">
        <template #reference>
          <el-button data-testid="popconfirm-basic" type="danger">Delete</el-button>
        </template>
      </el-popconfirm>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (confirm / cancel)</h3>
      <el-popconfirm
        title="Are you sure?"
        @confirm="onConfirm"
        @cancel="onCancel"
      >
        <template #reference>
          <el-button data-testid="popconfirm-interact" type="danger">Interact Delete</el-button>
        </template>
      </el-popconfirm>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (icon toggle)</h3>
      <el-button data-testid="popconfirm-toggle-icon" @click="toggleIcon">
        Toggle icon: <span data-testid="state-indicator">{{ useDelete ? 'Delete' : 'QuestionFilled' }}</span>
      </el-button>
      <el-popconfirm
        :title="`Icon=${useDelete ? 'Delete' : 'QuestionFilled'}`"
        :icon="useDelete ? Delete : QuestionFilled"
        icon-color="#f56c6c"
      >
        <template #reference>
          <el-button data-testid="popconfirm-state-target">Target</el-button>
        </template>
      </el-popconfirm>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { Delete, QuestionFilled } from '@element-plus/icons-vue'

const pickedValue = ref('(none)')
const useDelete = ref(true)

function onConfirm() { pickedValue.value = 'confirmed' }
function onCancel() { pickedValue.value = 'cancelled' }
function toggleIcon() { useDelete.value = !useDelete.value }
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

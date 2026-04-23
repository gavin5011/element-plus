<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Upload Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-upload
        data-testid="upload-basic"
        action="https://example.com/mock-upload"
        :auto-upload="false"
      >
        <el-button type="primary">Select File</el-button>
      </el-upload>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (drag-drop area)</h3>
      <el-upload
        data-testid="upload-interact"
        drag
        action="https://example.com/mock-upload"
        :auto-upload="false"
        :on-change="onChange"
      >
        <div class="el-upload__text">Drop file here or click to upload</div>
      </el-upload>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (multiple vs single)</h3>
      <el-button data-testid="upload-toggle-multiple" @click="multiple = !multiple">
        Toggle multiple: <span data-testid="state-indicator">{{ multiple ? 'multiple' : 'single' }}</span>
      </el-button>
      <el-upload
        data-testid="upload-state-target"
        :multiple="multiple"
        action="https://example.com/mock-upload"
        :auto-upload="false"
      >
        <el-button>Pick {{ multiple ? 'files' : 'file' }}</el-button>
      </el-upload>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { UploadFile } from 'element-plus'

const pickedValue = ref('(none)')
const multiple = ref(false)

function onChange(file: UploadFile) {
  pickedValue.value = file?.name ?? '(unknown)'
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

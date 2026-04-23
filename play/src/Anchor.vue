<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Anchor Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-anchor data-testid="anchor-basic" :offset="20">
        <el-anchor-link href="#a-basic" title="Section A" />
        <el-anchor-link href="#b-basic" title="Section B" />
        <el-anchor-link href="#c-basic" title="Section C" />
      </el-anchor>
      <div class="anchor-targets">
        <div id="a-basic" class="anchor-block">Section A content</div>
        <div id="b-basic" class="anchor-block">Section B content</div>
        <div id="c-basic" class="anchor-block">Section C content</div>
      </div>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (click link)</h3>
      <el-anchor
        data-testid="anchor-interact"
        :offset="20"
        @click="onClick"
      >
        <el-anchor-link href="#a" title="Section A" />
        <el-anchor-link href="#b" title="Section B" />
        <el-anchor-link href="#c" title="Section C" />
      </el-anchor>
      <div class="anchor-targets">
        <div id="a" class="anchor-block">Section A content</div>
        <div id="b" class="anchor-block">Section B content</div>
        <div id="c" class="anchor-block">Section C content</div>
      </div>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedHref || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (orientation)</h3>
      <el-button data-testid="anchor-toggle-orientation" @click="horizontal = !horizontal">
        Toggle orientation: <span data-testid="state-indicator">{{ horizontal ? 'horizontal' : 'vertical' }}</span>
      </el-button>
      <el-anchor
        data-testid="anchor-state-target"
        :offset="20"
        :direction="horizontal ? 'horizontal' : 'vertical'"
      >
        <el-anchor-link href="#a-state" title="Section A" />
        <el-anchor-link href="#b-state" title="Section B" />
        <el-anchor-link href="#c-state" title="Section C" />
      </el-anchor>
      <div class="anchor-targets">
        <div id="a-state" class="anchor-block">Section A content</div>
        <div id="b-state" class="anchor-block">Section B content</div>
        <div id="c-state" class="anchor-block">Section C content</div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pickedHref = ref('')
const horizontal = ref(false)

function onClick(e: MouseEvent, link: { href: string }) {
  pickedHref.value = link?.href ?? ''
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
.anchor-targets { width: 100%; display: flex; flex-direction: column; gap: 120px; margin-top: 12px; }
.anchor-block { padding: 16px; border: 1px dashed #dcdfe6; background: #fafafa; }
</style>

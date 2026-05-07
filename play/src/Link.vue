<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Link Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-link data-testid="link-basic" href="#">Default link</el-link>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="link-toggle-disabled"
        @click="linkDisabled = !linkDisabled"
        >Toggle</el-button
      ><el-link :disabled="linkDisabled" data-testid="link-interact" href="#"
        >Toggleable</el-link
      >
      <div data-testid="picked-value-display">
        Disabled:
        <span data-testid="picked-value">{{ String(linkDisabled) }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="link-cycle-type"
        @click="linkType = linkType === 'primary' ? 'success' : 'primary'"
        >Type:
        <span data-testid="state-indicator">{{ linkType }}</span></el-button
      ><el-link :type="linkType" data-testid="link-state-target" href="#">{{
        linkType
      }}</el-link>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const linkDisabled = ref(false)
const linkType = ref('primary')
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

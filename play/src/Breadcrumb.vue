<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Breadcrumb Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-breadcrumb separator="/" data-testid="breadcrumb-basic"
        ><el-breadcrumb-item>Home</el-breadcrumb-item
        ><el-breadcrumb-item>Page</el-breadcrumb-item></el-breadcrumb
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="breadcrumb-add-segment"
        @click="bcSegments.push(`L${bcSegments.length + 1}`)"
        >Add</el-button
      ><el-breadcrumb separator="/" data-testid="breadcrumb-interact"
        ><el-breadcrumb-item v-for="(s, i) in bcSegments" :key="i">{{
          s
        }}</el-breadcrumb-item></el-breadcrumb
      >
      <div data-testid="picked-value-display">
        Depth: <span data-testid="picked-value">{{ bcSegments.length }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="breadcrumb-toggle-separator"
        @click="bcSep = bcSep === '/' ? '>' : '/'"
        >Sep: <span data-testid="state-indicator">{{ bcSep }}</span></el-button
      ><el-breadcrumb :separator="bcSep" data-testid="breadcrumb-state-target"
        ><el-breadcrumb-item>A</el-breadcrumb-item
        ><el-breadcrumb-item>B</el-breadcrumb-item></el-breadcrumb
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const bcSegments = ref(['Home', 'Sub'])
const bcSep = ref('/')
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

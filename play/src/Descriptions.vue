<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Descriptions Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-descriptions
        title="Basic"
        :column="2"
        data-testid="descriptions-basic"
        ><el-descriptions-item label="Name">Alice</el-descriptions-item
        ><el-descriptions-item label="Age"
          >30</el-descriptions-item
        ></el-descriptions
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button data-testid="descriptions-add-item" @click="descCount++"
        >Add</el-button
      ><el-descriptions
        title="Interact"
        :column="2"
        data-testid="descriptions-interact"
        ><el-descriptions-item v-for="i in descCount" :key="i" :label="`F${i}`"
          >V{{ i }}</el-descriptions-item
        ></el-descriptions
      >
      <div data-testid="picked-value-display">
        Count: <span data-testid="picked-value">{{ descCount }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="descriptions-toggle-border"
        @click="descBorder = !descBorder"
        >Border:
        <span data-testid="state-indicator">{{
          descBorder ? 'on' : 'off'
        }}</span></el-button
      ><el-descriptions
        :border="descBorder"
        data-testid="descriptions-state-target"
        ><el-descriptions-item label="Test"
          >val</el-descriptions-item
        ></el-descriptions
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const descCount = ref(2)
const descBorder = ref(false)
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

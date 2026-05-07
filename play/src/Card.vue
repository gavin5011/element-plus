<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Card Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-card data-testid="card-basic" header="Basic Card"
        >Card body content</el-card
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button
        data-testid="card-toggle-shadow"
        @click="cardShadow = cardShadow === 'always' ? 'hover' : 'always'"
        >Shadow</el-button
      ><el-card
        :shadow="cardShadow"
        data-testid="card-interact"
        :header="`shadow=${cardShadow}`"
        >Body</el-card
      >
      <div data-testid="picked-value-display">
        Shadow: <span data-testid="picked-value">{{ cardShadow }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="card-cycle-bodysize"
        @click="cardBodyClass = cardBodyClass === 'small' ? 'large' : 'small'"
        >Body:
        <span data-testid="state-indicator">{{
          cardBodyClass
        }}</span></el-button
      ><el-card
        :body-class="`body-${cardBodyClass}`"
        data-testid="card-state-target"
        >{{ cardBodyClass }} body</el-card
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const cardShadow = ref('always')
const cardBodyClass = ref('small')
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

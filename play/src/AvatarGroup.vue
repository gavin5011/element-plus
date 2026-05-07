<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">AvatarGroup Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-avatar-group data-testid="avatar-group-basic"
        ><el-avatar>A</el-avatar><el-avatar>B</el-avatar
        ><el-avatar>C</el-avatar></el-avatar-group
      >
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Primary Interaction</h3>
      <el-button data-testid="avatar-group-add" @click="avatarCount++"
        >Add</el-button
      ><el-avatar-group data-testid="avatar-group-interact"
        ><el-avatar v-for="i in avatarCount" :key="i">{{
          i
        }}</el-avatar></el-avatar-group
      >
      <div data-testid="picked-value-display">
        Count: <span data-testid="picked-value">{{ avatarCount }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation</h3>
      <el-button
        data-testid="avatar-group-toggle-max"
        @click="avatarMax = avatarMax === 3 ? 5 : 3"
        >Max:
        <span data-testid="state-indicator">{{ avatarMax }}</span></el-button
      ><el-avatar-group :max="avatarMax" data-testid="avatar-group-state-target"
        ><el-avatar v-for="i in 6" :key="i">{{ i }}</el-avatar></el-avatar-group
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const avatarCount = ref(3)
const avatarMax = ref(3)
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

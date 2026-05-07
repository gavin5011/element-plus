<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Menu Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-menu data-testid="menu-basic" mode="horizontal" default-active="1">
        <el-menu-item index="1">Home</el-menu-item>
        <el-menu-item index="2">About</el-menu-item>
        <el-menu-item index="3">Services</el-menu-item>
        <el-menu-item index="4">Contact</el-menu-item>
        <el-sub-menu index="5">
          <template #title>More</template>
          <el-menu-item index="5-1">Docs</el-menu-item>
          <el-menu-item index="5-2">API</el-menu-item>
          <el-menu-item index="5-3">Support</el-menu-item>
        </el-sub-menu>
      </el-menu>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Select item)</h3>
      <el-menu
        data-testid="menu-interact"
        mode="horizontal"
        :default-active="pickedValue"
        @select="onSelect"
      >
        <el-menu-item index="1">Home</el-menu-item>
        <el-menu-item index="2">About</el-menu-item>
        <el-menu-item index="3">Services</el-menu-item>
        <el-menu-item index="4">Contact</el-menu-item>
        <el-sub-menu index="5">
          <template #title>More</template>
          <el-menu-item index="5-1">Docs</el-menu-item>
          <el-menu-item index="5-2">API</el-menu-item>
          <el-menu-item index="5-3">Support</el-menu-item>
        </el-sub-menu>
      </el-menu>
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (collapse toggle)</h3>
      <el-button
        data-testid="menu-toggle-collapse"
        @click="collapse = !collapse"
      >
        Toggle collapse:
        <span data-testid="state-indicator">{{
          collapse ? 'collapsed' : 'expanded'
        }}</span>
      </el-button>
      <div style="width: 220px">
        <el-menu
          data-testid="menu-state-target"
          mode="vertical"
          :collapse="collapse"
          default-active="1"
        >
          <el-menu-item index="1">Home</el-menu-item>
          <el-menu-item index="2">About</el-menu-item>
          <el-menu-item index="3">Services</el-menu-item>
          <el-menu-item index="4">Contact</el-menu-item>
          <el-sub-menu index="5">
            <template #title>More</template>
            <el-menu-item index="5-1">Docs</el-menu-item>
            <el-menu-item index="5-2">API</el-menu-item>
            <el-menu-item index="5-3">Support</el-menu-item>
          </el-sub-menu>
        </el-menu>
      </div>
    </section>

    <section data-testid="scenario-cat4-menu-item-nesting">
      <h3>
        S4: cat4 fixture - Menu item nesting depth drift (post-freeze refactor)
      </h3>
      <p>
        Spec was frozen with direct-child selector
        <code>data-testid="menu-item-settings"</code> at top-level menu. UI
        refactor wraps it under a submenu, so the spec's flat path no longer
        resolves; new testid
        <code>data-testid="cat4-menu-item-nesting-menu-item-settings"</code>
        lives nested.
      </p>
      <el-menu data-testid="cat4-menu-item-nesting-root" mode="horizontal">
        <el-sub-menu
          index="cat4-nest"
          data-testid="cat4-menu-item-nesting-submenu"
        >
          <template #title>Settings</template>
          <el-menu-item
            index="cat4-nest-1"
            data-testid="cat4-menu-item-nesting-menu-item-settings"
            >Nested Settings</el-menu-item
          >
        </el-sub-menu>
      </el-menu>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const pickedValue = ref('1')
const collapse = ref(false)

function onSelect(index: string) {
  pickedValue.value = index
}
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

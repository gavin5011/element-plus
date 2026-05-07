<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Dropdown Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-dropdown data-testid="dropdown-basic">
        <el-button data-testid="dropdown-trigger" type="primary">
          Actions
        </el-button>
        <template #dropdown>
          <el-dropdown-menu data-testid="dropdown-menu">
            <el-dropdown-item data-testid="item-edit">Edit</el-dropdown-item>
            <el-dropdown-item data-testid="item-copy">Copy</el-dropdown-item>
            <el-dropdown-item data-testid="item-delete" divided
              >Delete</el-dropdown-item
            >
          </el-dropdown-menu>
        </template>
      </el-dropdown>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click-triggered selection)</h3>
      <el-dropdown
        trigger="click"
        data-testid="dropdown-click"
        @command="handleCommand"
      >
        <el-button data-testid="dropdown-click-trigger">
          Selected: <span data-testid="dropdown-value">{{ selected }}</span>
        </el-button>
        <template #dropdown>
          <el-dropdown-menu>
            <el-dropdown-item command="Small" data-testid="opt-small"
              >Small</el-dropdown-item
            >
            <el-dropdown-item command="Medium" data-testid="opt-medium"
              >Medium</el-dropdown-item
            >
            <el-dropdown-item command="Large" data-testid="opt-large"
              >Large</el-dropdown-item
            >
          </el-dropdown-menu>
        </template>
      </el-dropdown>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (disabled toggle)</h3>
      <el-button
        data-testid="dropdown-toggle-disabled"
        @click="dropdownDisabled = !dropdownDisabled"
      >
        Toggle disabled:
        <span data-testid="state-indicator">{{
          dropdownDisabled ? 'disabled' : 'enabled'
        }}</span>
      </el-button>
      <el-dropdown
        :disabled="dropdownDisabled"
        data-testid="dropdown-state-target"
      >
        <el-button data-testid="dropdown-state-trigger">
          State trigger ({{ dropdownDisabled ? 'off' : 'on' }})
        </el-button>
        <template #dropdown>
          <el-dropdown-menu>
            <el-dropdown-item>A</el-dropdown-item>
            <el-dropdown-item>B</el-dropdown-item>
          </el-dropdown-menu>
        </template>
      </el-dropdown>
    </section>

    <section data-testid="scenario-cat4-dropdown-option-removal">
      <h3>
        S4: cat4 fixture - Dropdown option testid removal (post-freeze refactor)
      </h3>
      <p>
        Spec was frozen with selector <code>data-testid="opt-export"</code>. UI
        refactor removed the testid attribute; only
        <code>name="export"</code> remains. Spec selector no longer resolves.
      </p>
      <el-dropdown data-testid="cat4-dropdown-option-removal-dropdown">
        <el-button>Actions</el-button>
        <template #dropdown>
          <el-dropdown-menu>
            <el-dropdown-item name="export"
              >Export (testid removed)</el-dropdown-item
            >
            <el-dropdown-item name="import">Import</el-dropdown-item>
          </el-dropdown-menu>
        </template>
      </el-dropdown>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const selected = ref('Medium')
function handleCommand(cmd: string) {
  selected.value = cmd
}

const dropdownDisabled = ref(false)
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

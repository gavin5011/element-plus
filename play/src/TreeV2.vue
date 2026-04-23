<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">TreeV2 Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tree-v2
        data-testid="treev2-basic"
        :data="treeData"
        :height="240"
        :props="treeProps"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click node)</h3>
      <el-tree-v2
        data-testid="treev2-interact"
        :data="treeData"
        :height="240"
        :props="treeProps"
        @node-click="onNodeClick"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (checkbox toggle)</h3>
      <el-button data-testid="treev2-toggle-showCheckbox" @click="showCheckbox = !showCheckbox">
        Toggle checkbox: <span data-testid="state-indicator">{{ showCheckbox ? 'checkbox' : 'plain' }}</span>
      </el-button>
      <el-tree-v2
        data-testid="treev2-state-target"
        :data="treeData"
        :height="240"
        :props="treeProps"
        :show-checkbox="showCheckbox"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Node = { id: string; label: string; children?: Node[] }

const treeProps = { value: 'id', label: 'label', children: 'children' }

function buildTree(): Node[] {
  const roots: Node[] = []
  for (let i = 0; i < 5; i++) {
    const parent: Node = { id: `p-${i}`, label: `Parent ${i}`, children: [] }
    for (let j = 0; j < 9; j++) {
      parent.children!.push({ id: `p-${i}-c-${j}`, label: `Child ${i}-${j}` })
    }
    roots.push(parent)
  }
  return roots
}

const treeData = buildTree()
const pickedValue = ref('')
const showCheckbox = ref(false)

function onNodeClick(data: Node) {
  pickedValue.value = data.label
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

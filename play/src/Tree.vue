<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Tree Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-tree data-testid="tree-basic" :data="treeData" node-key="id" />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Click node)</h3>
      <el-tree
        data-testid="tree-interact"
        :data="treeData"
        node-key="id"
        @node-click="onNodeClick"
      />
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (draggable toggle)</h3>
      <el-button
        data-testid="tree-toggle-draggable"
        @click="draggable = !draggable"
      >
        Toggle draggable:
        <span data-testid="state-indicator">{{
          draggable ? 'draggable' : 'static'
        }}</span>
      </el-button>
      <el-tree
        data-testid="tree-state-target"
        :data="treeData"
        node-key="id"
        :draggable="draggable"
      />
    </section>

    <section data-testid="scenario-lazy">
      <h3>S4: Lazy load (cat 6 fixture)</h3>
      <el-button data-testid="tree-lazy-show" @click="lazyShown = true"
        >Show lazy tree</el-button
      >
      <el-tree
        v-if="lazyShown"
        data-testid="tree-lazy"
        :load="loadLazy"
        lazy
        node-key="id"
        :props="{ children: 'children', label: 'label', isLeaf: 'isLeaf' }"
      />
    </section>

    <section data-testid="scenario-cat4-tree-node-class-to-role">
      <h3>
        S4: cat4 fixture - Tree node selector class → role drift (post-freeze
        refactor)
      </h3>
      <p>
        Spec was frozen with class-based selector
        <code>.tree-node-leaf</code> (or
        <code>data-testid="tree-node-leaf"</code>). UI refactor removed the
        class and rely on <code>[role="treeitem"]</code> with new testid
        <code>data-testid="cat4-tree-node-class-to-role-treeitem"</code>. Spec
        selector no longer resolves.
      </p>
      <div class="cat4-tree-node-row">
        <span
          role="treeitem"
          data-testid="cat4-tree-node-class-to-role-treeitem"
          >Tree leaf (refactored to role)</span
        >
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Node = { id: string; label: string; children?: Node[] }

const treeData: Node[] = [
  {
    id: 'asia',
    label: 'Asia',
    children: [
      {
        id: 'jp',
        label: 'Japan',
        children: [
          { id: 'tokyo', label: 'Tokyo' },
          { id: 'osaka', label: 'Osaka' },
        ],
      },
      {
        id: 'cn',
        label: 'China',
        children: [
          { id: 'beijing', label: 'Beijing' },
          { id: 'shanghai', label: 'Shanghai' },
        ],
      },
    ],
  },
  {
    id: 'europe',
    label: 'Europe',
    children: [
      {
        id: 'de',
        label: 'Germany',
        children: [{ id: 'berlin', label: 'Berlin' }],
      },
      {
        id: 'fr',
        label: 'France',
        children: [{ id: 'paris', label: 'Paris' }],
      },
    ],
  },
  {
    id: 'americas',
    label: 'Americas',
    children: [
      {
        id: 'us',
        label: 'USA',
        children: [
          { id: 'nyc', label: 'New York' },
          { id: 'la', label: 'Los Angeles' },
        ],
      },
      { id: 'br', label: 'Brazil', children: [{ id: 'rio', label: 'Rio' }] },
    ],
  },
]

const pickedValue = ref('')
const draggable = ref(false)
const lazyShown = ref(false)

function onNodeClick(data: Node) {
  pickedValue.value = data.label
}

type LazyNode = { label: string; isLeaf?: boolean; level: number }
function loadLazy(
  node: { level: number; data: LazyNode | unknown },
  resolve: (data: LazyNode[]) => void
) {
  if (node.level === 0) {
    setTimeout(
      () =>
        resolve([
          { label: 'Asia (lazy)', isLeaf: false, level: 1 },
          { label: 'Europe (lazy)', isLeaf: false, level: 1 },
        ]),
      1000
    )
    return
  }
  setTimeout(
    () =>
      resolve([{ label: 'Tokyo (lazy)', isLeaf: true, level: node.level + 1 }]),
    1000
  )
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

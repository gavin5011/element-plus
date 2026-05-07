<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">VirtualList Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <p data-testid="virtual-list-basic-info">
        VirtualList scenario stub for cat5 capability gap fixture.
      </p>
      <ul>
        <li
          v-for="(item, i) in initialItems"
          :key="i"
          data-testid="virtual-list-basic-item"
        >
          {{ item }}
        </li>
      </ul>
    </section>

    <section data-testid="scenario-cat5-tosorted-capability-gap">
      <h3>
        S4: cat5 fixture — VirtualList Array.prototype.toSorted() capability gap
      </h3>
      <p>
        Mutation: scenario sort uses `Array.prototype.toSorted()` which was
        added in Chrome 110 (V8 11.0). - Chrome 84 (V8 8.4): NOT supported →
        TypeError → cat5 fires - Edge 92 (Chromium 92, V8 9.2): NOT supported →
        cat5 fires - Chrome 114 (V8 11.4): supported → spec passes (skip on this
        project)
      </p>
      <el-button data-testid="cat5-virtual-list-sort-button" @click="cat5Sort"
        >Sort with toSorted</el-button
      >
      <ul>
        <li
          v-if="sortedItems.length === 0"
          data-testid="cat5-virtual-list-empty"
        >
          (not yet sorted)
        </li>
        <li
          v-else
          v-for="(item, i) in sortedItems"
          :key="i"
          :data-testid="i === 0 ? 'cat5-virtual-list-first-item' : undefined"
        >
          {{ item }}
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const initialItems = ['gamma', 'beta', 'alpha', 'delta']
const sortedItems = ref<string[]>([])

function cat5Sort() {
  // cat5 mutation: use Array.prototype.toSorted (Chrome 110+ only).
  // On Chrome 84 / Edge 92 (Chromium 92), this throws TypeError: arr.toSorted is not a function
  // → cat5 capability gap fires.
  // The unconditional call is INTENTIONAL to surface the capability gap as a runtime error
  // (NOT guarded with feature detection — that would defeat the cat5 fixture purpose).
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  const arr: any[] = [...initialItems]
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  sortedItems.value = (arr as any).toSorted()
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
ul {
  list-style: none;
  padding-left: 0;
  width: 100%;
}
li {
  margin: 4px 0;
  padding: 4px 8px;
  background: #f5f7fa;
  border-radius: 2px;
}
</style>

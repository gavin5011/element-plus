<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Pagination Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-pagination
        data-testid="pagination-basic"
        :total="100"
        :page-size="10"
        :current-page="1"
        layout="prev, pager, next"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Change page)</h3>
      <el-pagination
        data-testid="pagination-interact"
        v-model:current-page="currentPage"
        :total="100"
        :page-size="10"
        layout="prev, pager, next"
        @current-change="onCurrentChange"
      />
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ currentPage }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (size toggle)</h3>
      <el-button data-testid="pagination-toggle-small" @click="small = !small">
        Toggle size: <span data-testid="state-indicator">{{ small ? 'small' : 'default' }}</span>
      </el-button>
      <el-pagination
        data-testid="pagination-state-target"
        :total="100"
        :page-size="10"
        :current-page="1"
        :small="small"
        layout="prev, pager, next"
      />
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const currentPage = ref(1)
const small = ref(false)

function onCurrentChange(page: number) {
  currentPage.value = page
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

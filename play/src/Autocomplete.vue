<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Autocomplete Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-autocomplete
        data-testid="autocomplete-basic"
        v-model="basicValue"
        :fetch-suggestions="querySuggestions"
        placeholder="Type a fruit"
      />
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (Type → select suggestion)</h3>
      <el-autocomplete
        data-testid="autocomplete-interact"
        v-model="pickedValue"
        :fetch-suggestions="querySuggestions"
        placeholder="Pick a fruit"
        clearable
      />
      <div data-testid="picked-value-display">
        Value:
        <span data-testid="picked-value">{{ pickedValue || '(none)' }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (remote simulation toggle)</h3>
      <el-button
        data-testid="autocomplete-toggle-remote"
        @click="remoteMode = !remoteMode"
      >
        Toggle remote:
        <span data-testid="state-indicator">{{
          remoteMode ? 'remote' : 'local'
        }}</span>
      </el-button>
      <el-autocomplete
        data-testid="autocomplete-state-target"
        v-model="stateValue"
        :fetch-suggestions="remoteMode ? queryRemote : querySuggestions"
        placeholder="Search"
      />
    </section>

    <section data-testid="scenario-cat6-autocomplete-debounce">
      <h3>
        S4: cat6 fixture - Autocomplete suggestions debounce 250ms (race vs
        same-session retry)
      </h3>
      <input
        data-testid="autocomplete-debounce-input"
        type="text"
        v-model="debounceQuery"
        @input="debounceHandler"
        placeholder="Type then wait 250ms"
        style="padding: 4px"
      />
      <ul v-if="debounceSuggestions.length > 0">
        <li
          v-for="(s, i) in debounceSuggestions"
          :key="i"
          :data-testid="`autocomplete-debounce-suggestion-${i}`"
        >
          {{ s }}
        </li>
      </ul>
    </section>

    <section data-testid="scenario-cat6-autocomplete-no-results-delay">
      <h3>
        S5: cat6 fixture - Autocomplete no-results delay 200ms (race vs
        same-session retry)
      </h3>
      <input
        data-testid="autocomplete-no-results-input"
        type="text"
        v-model="noResultsQuery"
        @input="noResultsHandler"
        placeholder="Type 'xyz' then wait 200ms"
        style="padding: 4px"
      />
      <span
        v-if="noResultsEmptyShown"
        data-testid="autocomplete-no-results-empty-state"
        >No results</span
      >
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

type Suggestion = { value: string }
type Cb = (results: Suggestion[]) => void

const fruits: Suggestion[] = [
  { value: 'Apple' },
  { value: 'Banana' },
  { value: 'Cherry' },
  { value: 'Date' },
  { value: 'Elderberry' },
]

const querySuggestions = (query: string, cb: Cb) => {
  const results = query
    ? fruits.filter((f) => f.value.toLowerCase().includes(query.toLowerCase()))
    : fruits
  cb(results)
}

const queryRemote = (query: string, cb: Cb) => {
  setTimeout(() => {
    const results = query
      ? fruits.filter((f) =>
          f.value.toLowerCase().includes(query.toLowerCase())
        )
      : fruits
    cb(results)
  }, 1200)
}

const basicValue = ref('')
const pickedValue = ref('')
const stateValue = ref('')
const remoteMode = ref(false)

// cat6 fixtures
const debounceQuery = ref('')
const debounceSuggestions = ref<string[]>([])
let debounceTimer: ReturnType<typeof setTimeout> | null = null
function debounceHandler() {
  if (debounceTimer) clearTimeout(debounceTimer)
  debounceTimer = setTimeout(() => {
    const q = debounceQuery.value
    debounceSuggestions.value = q
      ? fruits
          .map((f) => f.value)
          .filter((v) => v.toLowerCase().includes(q.toLowerCase()))
      : []
  }, 250)
}

const noResultsQuery = ref('')
const noResultsEmptyShown = ref(false)
let noResultsTimer: ReturnType<typeof setTimeout> | null = null
function noResultsHandler() {
  if (noResultsTimer) clearTimeout(noResultsTimer)
  noResultsEmptyShown.value = false
  noResultsTimer = setTimeout(() => {
    const q = noResultsQuery.value
    const matches = fruits
      .map((f) => f.value)
      .filter((v) => v.toLowerCase().includes(q.toLowerCase()))
    noResultsEmptyShown.value = q.length > 0 && matches.length === 0
  }, 200)
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

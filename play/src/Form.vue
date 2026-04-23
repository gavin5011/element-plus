<template>
  <div class="demo-page" data-testid="demo-root">
    <h2 data-testid="demo-title">Form Component</h2>

    <section data-testid="scenario-basic">
      <h3>S1: Basic Render</h3>
      <el-form data-testid="form-basic" :model="basicModel" label-width="80px">
        <el-form-item label="Name">
          <el-input v-model="basicModel.name" placeholder="Enter name" />
        </el-form-item>
        <el-form-item label="Email">
          <el-input v-model="basicModel.email" placeholder="Enter email" />
        </el-form-item>
        <el-form-item label="Age">
          <el-input-number v-model="basicModel.age" :min="0" :max="120" />
        </el-form-item>
      </el-form>
    </section>

    <section data-testid="scenario-interaction">
      <h3>S2: Interaction (fill + submit)</h3>
      <el-form
        ref="interactFormRef"
        data-testid="form-interact"
        :model="interactModel"
        :rules="interactRules"
        label-width="80px"
      >
        <el-form-item label="Name" prop="name">
          <el-input v-model="interactModel.name" placeholder="Name (required)" />
        </el-form-item>
        <el-form-item label="Email" prop="email">
          <el-input v-model="interactModel.email" placeholder="Email (required)" />
        </el-form-item>
        <el-form-item label="Age" prop="age">
          <el-input-number v-model="interactModel.age" :min="0" :max="120" />
        </el-form-item>
        <el-form-item>
          <el-button type="primary" data-testid="form-submit" @click="submitForm">Submit</el-button>
        </el-form-item>
      </el-form>
      <div data-testid="picked-value-display">
        Value: <span data-testid="picked-value">{{ submittedValue }}</span>
      </div>
    </section>

    <section data-testid="scenario-state">
      <h3>S3: State Variation (strict/loose validation)</h3>
      <el-button data-testid="form-toggle-strict" @click="strictMode = !strictMode">
        Toggle validation: <span data-testid="state-indicator">{{ strictMode ? 'strict' : 'loose' }}</span>
      </el-button>
      <el-form
        data-testid="form-state-target"
        :model="stateModel"
        :rules="strictMode ? strictRules : looseRules"
        label-width="80px"
      >
        <el-form-item label="Name" prop="name">
          <el-input v-model="stateModel.name" placeholder="Name" />
        </el-form-item>
        <el-form-item label="Email" prop="email">
          <el-input v-model="stateModel.email" placeholder="Email" />
        </el-form-item>
      </el-form>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'

const basicModel = reactive({ name: '', email: '', age: 18 })
const interactModel = reactive({ name: '', email: '', age: 18 })
const stateModel = reactive({ name: '', email: '' })

const interactRules: FormRules = {
  name: [{ required: true, message: 'Name required', trigger: 'blur' }],
  email: [{ required: true, type: 'email', message: 'Valid email required', trigger: 'blur' }],
  age: [{ required: true, type: 'number', min: 1, message: 'Age > 0', trigger: 'change' }],
}

const strictRules: FormRules = {
  name: [{ required: true, min: 3, message: 'Name min 3 chars', trigger: 'blur' }],
  email: [{ required: true, type: 'email', message: 'Valid email required', trigger: 'blur' }],
}
const looseRules: FormRules = {
  name: [{ required: false, trigger: 'blur' }],
  email: [{ required: false, trigger: 'blur' }],
}

const interactFormRef = ref<FormInstance>()
const submittedValue = ref('(none)')
const strictMode = ref(true)

const submitForm = async () => {
  if (!interactFormRef.value) return
  try {
    await interactFormRef.value.validate()
    submittedValue.value = `${interactModel.name} / ${interactModel.email} / ${interactModel.age}`
  } catch {
    submittedValue.value = '(validation failed)'
  }
}
</script>

<style scoped>
.demo-page { padding: 24px; font-family: system-ui; }
section { margin-top: 16px; display: flex; gap: 16px; align-items: center; flex-wrap: wrap; }
section h3 { width: 100%; margin-bottom: 8px; color: #606266; }
</style>

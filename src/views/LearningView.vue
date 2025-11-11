<script setup lang="ts">
import { ref, reactive } from 'vue'

// Define interfaces for type safety
interface User {
  name: string
  age: number
}

// Basic reactive examples with explicit types
const count = ref<number>(0)
const items: string[] = ['Apple', 'Banana', 'Cherry']

const increment = (): void => {
  count.value++
  console.log('Increment button clicked', count.value)
}

const user = reactive<User>({
  name: 'Vineet',
  age: 30,
})

const incrementAge = (): void => {
  user.age++
}
</script>

<template>
  <div class="learning-page">
    <!-- Header -->
    <header class="header">
      <h1>🔥 Vue.js Learning Dashboard</h1>
      <p class="subtitle">From Basics to Pro-level with Real Industry Insights</p>
    </header>

    <!-- User Info Example -->
    <section class="card">
      <h2>🧍 Reactive Example (User)</h2>
      <p>{{ user.name }} ({{ user.age }})</p>
      <button class="btn" @click="incrementAge">Increase Age</button>
    </section>

    <!-- Basic Concepts -->
    <section class="card">
      <h2>🌱 Basic Concepts</h2>
      <pre class="code-block">
Template syntax → v-if, v-for, v-model
Two-way binding → v-model
Event handling → @click, @input
Interpolation → &#123;&#123; variable &#125;&#125;
List rendering → v-for
Conditional rendering → v-if / v-show

Example:
&lt;p v-if="count"&gt;Welcome back!&lt;/p&gt;
&lt;ul&gt;
  &lt;li v-for="item in items"&gt;&#123;&#123; item &#125;&#125;&lt;/li&gt;
&lt;/ul&gt;
      </pre>
    </section>

    <!-- React Comparison -->
    <section class="card">
      <h2>🔁 React vs Vue Quick Comparison</h2>
      <pre class="code-block">
React Hook → Vue Equivalent
------------------------------
useState → ref() or reactive()
useEffect → watch() / onMounted()
props → props (similar)
.map() → v-for
{ condition && &lt;div&gt;&lt;/div&gt; } → v-if
onChange + value → v-model
      </pre>
    </section>

    <!-- Lifecycle -->
    <section class="card">
      <h2>🔄 Lifecycle Hooks</h2>
      <pre class="code-block">
Hook                When it runs
----------------------------------------
onMounted()         After component is mounted
onUpdated()         When reactive data updates
onUnmounted()       When component is destroyed
onBeforeMount()     Before component mounts
onBeforeUpdate()    Before DOM updates
      </pre>
    </section>

    <!-- API Example -->
    <section class="card">
      <h2>🌐 API Calls Example (with async setup)</h2>
      <pre class="code-block">
import { ref, onMounted } from 'vue'

interface User {
  id: number
  name: string
  email: string
}

const users = ref&lt;User[]&gt;([])

onMounted(async () =&gt; {
  const res = await fetch('https://jsonplaceholder.typicode.com/users')
  users.value = await res.json()
})
      </pre>
    </section>

    <!-- Advanced Concepts -->
    <section class="card">
      <h2>🚀 Advanced Concepts</h2>
      <pre class="code-block">
1️⃣ Composition API (setup(), ref, reactive, computed)
2️⃣ Watchers (watch, watchEffect)
3️⃣ Provide / Inject (dependency sharing)
4️⃣ Reusable Composables (like useFetch.ts)
5️⃣ Dynamic Components
6️⃣ Teleport (render element outside root)
7️⃣ Slots (content distribution)
8️⃣ Transitions & Animations
9️⃣ Pinia or Vuex for State Management
🔟 Server-Side Rendering (Nuxt.js)
      </pre>
    </section>

    <!-- Industry Practices -->
    <section class="card">
      <h2>🏢 Industry Standard Practices</h2>
      <pre class="code-block">
✔️ Always use script setup with TypeScript
✔️ Use ESLint + Prettier for clean code
✔️ Follow component naming conventions (PascalCase)
✔️ Avoid mutating props directly
✔️ Use composables for reusable logic (e.g. useForm, useApi)
✔️ Lazy-load heavy routes
✔️ Use environment variables (.env)
✔️ Structure project:
  src/
   ├── components/
   ├── composables/
   ├── views/
   ├── store/
   ├── router/
   └── utils/
✔️ Keep templates clean (less than 100 lines)
✔️ Always handle API errors gracefully
✔️ Define proper TypeScript interfaces for all data
      </pre>
    </section>

    <!-- Common Mistakes -->
    <section class="card warning">
      <h2>⚠️ Common Mistakes Developers Make</h2>
      <pre class="code-block">
❌ Forgetting .value when using ref()
❌ Directly mutating props (causes warning)
❌ Forgetting to return reactive variables from setup()
❌ Overusing v-if (use v-show for toggling)
❌ Not using key with v-for
❌ Forgetting to cleanup in watch()
❌ Mixing Options API and Composition API incorrectly
❌ Deep watchers without care → performance issues
❌ Not defining TypeScript types for reactive data
❌ Using 'any' type instead of proper interfaces
      </pre>
    </section>

    <!-- Real Project Examples -->
    <section class="card">
      <h2>💼 Real Project Examples</h2>
      <pre class="code-block">
🧾 Form Handling:
  - Use v-model and composables for form validation
  - Example: useForm() hook with reactive state
  - Define interface FormData for type safety

📦 API Integration:
  - Create useApi composable for fetch + error + loading
  - Example:
    interface ApiResponse&lt;T&gt; {
      data: Ref&lt;T | null&gt;
      error: Ref&lt;Error | null&gt;
      loading: Ref&lt;boolean&gt;
    }
    const { data, error, loading } = useApi&lt;User[]&gt;('/users')

🔍 Search / Filter:
  - Use computed properties to filter data reactively
  - Type the computed return value properly

🌗 Theme / Dark Mode:
  - Store theme in Pinia or LocalStorage, apply via class binding
  - Use enum or union types for theme values
      </pre>
    </section>

    <!-- TypeScript Tips -->
    <section class="card">
      <h2>📘 TypeScript Tips for Vue</h2>
      <pre class="code-block">
// Ref with explicit type
const count = ref&lt;number&gt;(0)

// Reactive with interface
interface User {
  name: string
  age: number
}
const user = reactive&lt;User&gt;({ name: 'John', age: 30 })

// Props with TypeScript
interface Props {
  title: string
  count?: number
}
const props = defineProps&lt;Props&gt;()

// Emits with TypeScript
const emit = defineEmits&lt;{
  update: [value: string]
  delete: [id: number]
}&gt;()

// Computed with type inference
const doubled = computed(() =&gt; count.value * 2) // type: number

// Function with explicit return type
const fetchData = async (): Promise&lt;User[]&gt; =&gt; {
  const res = await fetch('/api/users')
  return res.json()
}
      </pre>
    </section>

    <!-- Motivation -->
    <section class="card footer">
      <h2>💡 Remember</h2>
      <p>
        "Vue is not just a framework — it's a way to think in reactive systems. Master reactivity,
        composables, TypeScript, and clean architecture — and you can build anything."
      </p>
    </section>
  </div>
</template>

<style scoped>
.learning-page {
  max-width: 1000px;
  margin: 2rem auto;
  padding: 1.5rem;
  font-family: 'Inter', sans-serif;
  color: #333;
  line-height: 1.6;
  background: #f8fafc;
}

.header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.header h1 {
  font-size: 2.3rem;
  color: #2563eb;
  margin-bottom: 0.25rem;
}

.subtitle {
  color: #64748b;
  font-size: 1rem;
}

.card {
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.04);
}

.card h2 {
  color: #1e293b;
  margin-bottom: 0.75rem;
}

.btn {
  background-color: #2563eb;
  color: white;
  border: none;
  border-radius: 6px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background 0.2s ease;
}
.btn:hover {
  background-color: #1d4ed8;
}

.code-block {
  background: #1e293b;
  color: #e2e8f0;
  border-radius: 8px;
  padding: 1rem;
  font-family: 'Fira Code', monospace;
  white-space: pre-wrap;
  overflow-x: auto;
  font-size: 0.9rem;
}

.warning {
  border-left: 5px solid #f97316;
  background: #fff7ed;
}

.footer {
  background: #f0f9ff;
  border: 1px solid #bae6fd;
  text-align: center;
}
</style>

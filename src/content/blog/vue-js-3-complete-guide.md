---
title: "Vue.js 3完全指南"
description: "学习Vue.js 3的基本概念、核心特性和最佳实践。"
date: 2024-03-06
tags: ["Vue.js", "前端框架", "JavaScript"]
author: "博客作者"
---

Vue.js 是一个渐进式 JavaScript 框架，用于构建用户界面。Vue.js 3 是 Vue.js 的最新版本，带来了许多新特性和性能改进。本文将介绍 Vue.js 3 的基本概念、核心特性和最佳实践，帮助你快速入门 Vue.js 3。

## Vue.js 3 的新特性

### 1. 组合式 API (Composition API)

组合式 API 是 Vue.js 3 的核心特性，它提供了一种更灵活的方式来组织和复用组件逻辑：

```vue
<template>
  <div>
    <h2>计数器: {{ count }}</h2>
    <button @click="increment">增加</button>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const count = ref(0);
const doubleCount = computed(() => count.value * 2);

function increment() {
  count.value++;
}
</script>
```

### 2. 响应式系统重构

Vue.js 3 使用 Proxy API 重写了响应式系统，带来了更好的性能和更完整的响应式支持：

```javascript
// Vue.js 3响应式系统
import { reactive, computed } from "vue";

const state = reactive({
  count: 0,
});

const doubleCount = computed(() => state.count * 2);

// 修改状态会自动更新视图
state.count++;
```

### 3. 性能改进

Vue.js 3 在性能方面有显著改进，包括：

- 更快的虚拟 DOM 算法
- 更小的打包体积
- 按需编译
- 更高效的组件渲染

### 4. TypeScript 支持

Vue.js 3 提供了更好的 TypeScript 支持，包括：

- 完全的类型定义
- 更好的类型推断
- 支持 TypeScript 装饰器

### 5. Teleport

Teleport 允许你将组件内容渲染到 DOM 树的任何位置：

```vue
<template>
  <div>
    <h2>Teleport示例</h2>
    <Teleport to="#modal-container">
      <div class="modal">
        <h3>模态框</h3>
        <p>这是一个模态框内容</p>
        <button @click="closeModal">关闭</button>
      </div>
    </Teleport>
    <button @click="openModal">打开模态框</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);

function openModal() {
  showModal.value = true;
}

function closeModal() {
  showModal.value = false;
}
</script>
```

### 6. Suspense

Suspense 允许你在组件加载完成前显示占位内容：

```vue
<template>
  <div>
    <h2>Suspense示例</h2>
    <Suspense>
      <template #default>
        <AsyncComponent />
      </template>
      <template #fallback>
        <div>加载中...</div>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import { defineAsyncComponent } from "vue";

const AsyncComponent = defineAsyncComponent(() =>
  import("./AsyncComponent.vue")
);
</script>
```

## Vue.js 3 基础

### 1. 安装 Vue.js 3

使用 npm 或 yarn 安装 Vue.js 3：

```bash
# 使用npm
npm create vue@latest

# 使用yarn
yarn create vue
```

### 2. 创建 Vue.js 3 项目

使用 Vue CLI 创建 Vue.js 3 项目：

```bash
# 创建Vue.js 3项目
npm create vue@latest my-vue-app
cd my-vue-app
npm install
npm run dev
```

### 3. 基本组件结构

Vue.js 3 组件的基本结构：

```vue
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script setup>
import { ref } from "vue";

const msg = ref("Hello Vue 3!");
</script>

<style scoped>
.hello {
  font-size: 2rem;
  color: #42b983;
}
</style>
```

## Vue.js 3 核心概念

### 1. 响应式数据

Vue.js 3 提供了 ref 和 reactive 两种方式来创建响应式数据：

```vue
<template>
  <div>
    <h2>响应式数据示例</h2>
    <p>计数: {{ count }}</p>
    <p>用户: {{ user.name }}</p>
    <p>用户邮箱: {{ user.email }}</p>
    <button @click="updateData">更新数据</button>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";

// 基本类型使用ref
const count = ref(0);

// 对象类型使用reactive
const user = reactive({
  name: "张三",
  email: "zhangsan@example.com",
});

function updateData() {
  count.value++;
  user.name = "李四";
  user.email = "lisi@example.com";
}
</script>
```

### 2. 计算属性

计算属性用于处理派生数据：

```vue
<template>
  <div>
    <h2>计算属性示例</h2>
    <p>原始价格: {{ price }}</p>
    <p>折扣价格: {{ discountedPrice }}</p>
    <p>是否有折扣: {{ hasDiscount }}</p>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const price = ref(100);
const discount = ref(0.2);

// 计算折扣价格
const discountedPrice = computed(() => {
  return price.value * (1 - discount.value);
});

// 计算是否有折扣
const hasDiscount = computed(() => {
  return discount.value > 0;
});
</script>
```

### 3. 监听器

监听器用于监听数据变化并执行副作用：

```vue
<template>
  <div>
    <h2>监听器示例</h2>
    <p>计数: {{ count }}</p>
    <p>上一次计数: {{ previousCount }}</p>
    <button @click="increment">增加</button>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const count = ref(0);
const previousCount = ref(0);

// 监听count变化
watch(count, (newVal, oldVal) => {
  previousCount.value = oldVal;
  console.log(`计数从 ${oldVal} 变化到 ${newVal}`);
});

function increment() {
  count.value++;
}
</script>
```

### 4. 生命周期钩子

Vue.js 3 提供了一系列生命周期钩子，用于在组件的不同阶段执行代码：

```vue
<template>
  <div>
    <h2>生命周期钩子示例</h2>
    <p>组件已经挂载</p>
  </div>
</template>

<script setup>
import { onMounted, onUpdated, onUnmounted } from "vue";

onMounted(() => {
  console.log("组件挂载完成");
});

onUpdated(() => {
  console.log("组件更新完成");
});

onUnmounted(() => {
  console.log("组件卸载完成");
});
</script>
```

### 5. 组件通信

Vue.js 3 提供了多种组件通信方式：

#### Props

```vue
<!-- 父组件 -->
<template>
  <div>
    <h2>父组件</h2>
    <ChildComponent :message="parentMessage" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import ChildComponent from "./ChildComponent.vue";

const parentMessage = ref("Hello from parent!");
</script>

<!-- 子组件 -->
<template>
  <div>
    <h3>子组件</h3>
    <p>{{ message }}</p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  message: String,
});
</script>
```

#### Emits

```vue
<!-- 父组件 -->
<template>
  <div>
    <h2>父组件</h2>
    <p>子组件消息: {{ childMessage }}</p>
    <ChildComponent @send-message="handleMessage" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import ChildComponent from "./ChildComponent.vue";

const childMessage = ref("");

function handleMessage(message) {
  childMessage.value = message;
}
</script>

<!-- 子组件 -->
<template>
  <div>
    <h3>子组件</h3>
    <button @click="sendMessage">发送消息</button>
  </div>
</template>

<script setup>
import { defineEmits } from "vue";

const emit = defineEmits(["send-message"]);

function sendMessage() {
  emit("send-message", "Hello from child!");
}
</script>
```

#### Provide/Inject

```vue
<!-- 父组件 -->
<template>
  <div>
    <h2>父组件</h2>
    <ChildComponent />
  </div>
</template>

<script setup>
import { ref, provide } from "vue";
import ChildComponent from "./ChildComponent.vue";

const theme = ref("dark");

// 提供数据
provide("theme", theme);
</script>

<!-- 子组件 -->
<template>
  <div>
    <h3>子组件</h3>
    <p>当前主题: {{ theme }}</p>
  </div>
</template>

<script setup>
import { inject } from "vue";

// 注入数据
const theme = inject("theme");
</script>
```

### 6. 路由

Vue.js 3 使用 Vue Router 4 进行路由管理：

```javascript
// router/index.js
import { createRouter, createWebHistory } from "vue-router";
import HomeView from "../views/HomeView.vue";
import AboutView from "../views/AboutView.vue";

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: "/",
      name: "home",
      component: HomeView,
    },
    {
      path: "/about",
      name: "about",
      component: AboutView,
    },
  ],
});

export default router;
```

```vue
<!-- App.vue -->
<template>
  <div>
    <nav>
      <router-link to="/">首页</router-link>
      <router-link to="/about">关于</router-link>
    </nav>
    <router-view />
  </div>
</template>

<script setup>
// App.vue 不需要额外的路由代码
</script>
```

### 7. 状态管理

Vue.js 3 可以使用 Pinia 进行状态管理：

```bash
# 安装Pinia
npm install pinia
```

```javascript
// main.js
import { createApp } from "vue";
import { createPinia } from "pinia";
import App from "./App.vue";
import router from "./router";

const app = createApp(App);
app.use(createPinia());
app.use(router);
app.mount("#app");
```

```javascript
// stores/counter.js
import { defineStore } from "pinia";

export const useCounterStore = defineStore("counter", {
  state: () => ({
    count: 0,
  }),
  getters: {
    doubleCount: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++;
    },
  },
});
```

```vue
<template>
  <div>
    <h2>计数器: {{ counter.count }}</h2>
    <h3>双倍计数: {{ counter.doubleCount }}</h3>
    <button @click="counter.increment">增加</button>
  </div>
</template>

<script setup>
import { useCounterStore } from "../stores/counter";

const counter = useCounterStore();
</script>
```

## Vue.js 3 最佳实践

### 1. 使用组合式 API 组织逻辑

```vue
<template>
  <div>
    <h2>用户列表</h2>
    <div v-if="loading">加载中...</div>
    <div v-else-if="error">错误: {{ error }}</div>
    <div v-else>
      <ul>
        <li v-for="user in users" :key="user.id">
          {{ user.name }} - {{ user.email }}
        </li>
      </ul>
    </div>
    <button @click="loadUsers">加载用户</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

// 提取用户列表逻辑
function useUsers() {
  const users = ref([]);
  const loading = ref(false);
  const error = ref(null);

  async function loadUsers() {
    try {
      loading.value = true;
      error.value = null;
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users"
      );
      users.value = await response.json();
    } catch (err) {
      error.value = err.message;
    } finally {
      loading.value = false;
    }
  }

  onMounted(() => {
    loadUsers();
  });

  return { users, loading, error, loadUsers };
}

// 使用用户列表逻辑
const { users, loading, error, loadUsers } = useUsers();
</script>
```

### 2. 使用 TypeScript

```vue
<template>
  <div>
    <h2>TypeScript示例</h2>
    <p>计数: {{ count }}</p>
    <button @click="increment">增加</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const count = ref<number>(0);

function increment(): void {
  count.value++;
}
</script>
```

### 3. 组件命名规范

使用 PascalCase 命名组件：

```
components/
├── UserList.vue
├── UserCard.vue
└── UserForm.vue
```

### 4. 目录结构

组织清晰的目录结构：

```
src/
├── assets/
├── components/
├── composables/
├── views/
├── router/
├── stores/
├── App.vue
└── main.js
```

### 5. 性能优化

#### 使用 v-memo

```vue
<template>
  <div>
    <h2>用户列表</h2>
    <ul>
      <li v-for="user in users" :key="user.id" v-memo="[user.name, user.email]">
        {{ user.name }} - {{ user.email }}
      </li>
    </ul>
  </div>
</template>
```

#### 使用 v-once

```vue
<template>
  <div>
    <h2>静态内容</h2>
    <div v-once>
      <p>这是静态内容，只会渲染一次</p>
      <p>{{ staticData }}</p>
    </div>
  </div>
</template>
```

#### 使用 keep-alive

```vue
<template>
  <div>
    <h2>路由缓存</h2>
    <router-view v-slot="{ Component }">
      <keep-alive>
        <component :is="Component" />
      </keep-alive>
    </router-view>
  </div>
</template>
```

## Vue.js 3 与其他框架的比较

### 1. Vue.js 3 vs React

| 特性     | Vue.js 3   | React              |
| -------- | ---------- | ------------------ |
| 学习曲线 | 平缓       | 较陡               |
| 模板语法 | HTML 模板  | JSX                |
| 状态管理 | Pinia      | Redux、Context API |
| 路由     | Vue Router | React Router       |
| 性能     | 高         | 高                 |
| 社区支持 | 大         | 特大               |

### 2. Vue.js 3 vs Angular

| 特性     | Vue.js 3 | Angular |
| -------- | -------- | ------- |
| 学习曲线 | 平缓     | 陡峭    |
| 体积     | 小       | 大      |
| 性能     | 高       | 中      |
| 灵活性   | 高       | 低      |
| 社区支持 | 大       | 大      |

## 总结

Vue.js 3 是一个功能强大、易于学习的 JavaScript 框架，它提供了组合式 API、响应式系统重构、性能改进等新特性，使得构建现代 Web 应用变得更加容易。通过学习 Vue.js 3 的基本概念、核心特性和最佳实践，你可以快速入门 Vue.js 3，并使用它构建高质量的 Web 应用。

随着 Vue.js 3 的不断发展和普及，它已经成为现代前端开发的重要框架之一，建议你在新项目中使用 Vue.js 3，并逐步将旧项目迁移到 Vue.js 3。

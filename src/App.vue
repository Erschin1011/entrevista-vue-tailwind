<script setup>
import { computed, ref } from 'vue'

const tasks = ref([
  { id: 1, title: 'Revisar el enunciado y definir el modelo', done: true },
  { id: 2, title: 'Implementar la funcionalidad principal', done: false },
])
const newTask = ref('')
const pendingCount = computed(() => tasks.value.filter((task) => !task.done).length)

function addTask() {
  const title = newTask.value.trim()
  if (!title) return
  tasks.value.push({ id: Date.now(), title, done: false })
  newTask.value = ''
}

function removeTask(id) {
  tasks.value = tasks.value.filter((task) => task.id !== id)
}
</script>

<template>
  <main class="mx-auto max-w-3xl px-5 py-12 sm:py-20">
    <header class="mb-9">
      <p class="mb-3 text-sm font-semibold uppercase tracking-[0.18em] text-indigo-600">Vue 3 · JavaScript · Tailwind CSS 4</p>
      <h1 class="text-4xl font-bold tracking-tight text-slate-900 sm:text-5xl">Interview starter</h1>
      <p class="mt-3 max-w-2xl text-lg text-slate-600">Plantilla lista para clonar y convertir rápidamente en la solución del ejercicio técnico.</p>
    </header>

    <section class="rounded-2xl border border-slate-200 bg-white p-5 shadow-sm sm:p-7">
      <div class="mb-5 flex items-center justify-between gap-3">
        <div>
          <h2 class="text-xl font-semibold text-slate-900">Lista de tareas de ejemplo</h2>
          <p class="mt-1 text-sm text-slate-500">{{ pendingCount }} pendiente(s) · estado con <code class="rounded bg-slate-100 px-1.5 py-0.5 text-xs">ref</code></p>
        </div>
        <span class="rounded-full bg-indigo-50 px-3 py-1 text-sm font-medium text-indigo-700">demo</span>
      </div>

      <form class="flex flex-col gap-2 sm:flex-row" @submit.prevent="addTask">
        <input v-model="newTask" class="min-w-0 flex-1 rounded-lg border border-slate-300 px-3 py-2.5 outline-none transition placeholder:text-slate-400 focus:border-indigo-500 focus:ring-4 focus:ring-indigo-100" placeholder="Escribe una tarea..." aria-label="Nueva tarea" />
        <button class="rounded-lg bg-indigo-600 px-4 py-2.5 font-semibold text-white transition hover:bg-indigo-700 focus:outline-none focus:ring-4 focus:ring-indigo-200">Agregar tarea</button>
      </form>

      <ul class="mt-5 divide-y divide-slate-100">
        <li v-for="task in tasks" :key="task.id" class="flex items-center gap-3 py-3">
          <input v-model="task.done" type="checkbox" class="size-4 accent-indigo-600" :aria-label="`Completar ${task.title}`" />
          <span class="flex-1 text-slate-700" :class="{ 'text-slate-400 line-through': task.done }">{{ task.title }}</span>
          <button class="rounded px-2 py-1 text-sm text-slate-500 hover:bg-rose-50 hover:text-rose-700" type="button" @click="removeTask(task.id)">Quitar</button>
        </li>
      </ul>
    </section>

    <section class="mt-6 grid gap-4 sm:grid-cols-3">
      <article class="rounded-xl border border-slate-200 bg-white p-4"><p class="text-sm font-semibold text-slate-900">Componentes</p><p class="mt-1 text-sm text-slate-600">Divide interfaz por responsabilidad.</p></article>
      <article class="rounded-xl border border-slate-200 bg-white p-4"><p class="text-sm font-semibold text-slate-900">Estado</p><p class="mt-1 text-sm text-slate-600">Practica <code>ref</code> y <code>computed</code>.</p></article>
      <article class="rounded-xl border border-slate-200 bg-white p-4"><p class="text-sm font-semibold text-slate-900">Estilos</p><p class="mt-1 text-sm text-slate-600">Utilidades Tailwind, sin CSS framework extra.</p></article>
    </section>

    <footer class="mt-8 text-sm text-slate-500">Comandos: <code>npm install</code> · <code>npm run dev</code> · <code>npm run build</code></footer>
  </main>
</template>

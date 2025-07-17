<template>
  <div class="drawer lg:drawer-open font-display">
    <input type="checkbox" id="my-drawer" class="drawer-toggle" />
    <!-- Page Content -->
    <div class="drawer-content flex flex-col">
      <Navbar :is-dark="isDark" @toggle-drawer="toggleDrawer" @toggle-theme="toggleTheme"/>
      <main class="flex-1 p-6 bg-base-200 dark:bg-backgroundDark">
        <StatsCards />
        <Charts />
      </main>
    </div>
    <!-- Sidebar -->
    <Sidebar />
  </div>
</template>
<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import Navbar from './components/layout/Navbar.vue';
import Sidebar from './components/layout/Sidebar.vue';
import StatsCards from './components/layout/StatsCards.vue';
import Charts from './components/layout/Charts.vue';

const isDark = ref<boolean>(false);

// Aplica o tema salvo assim que o script roda (antes do Vue montar)
const savedTheme = localStorage.getItem('theme-dashboard');
if (savedTheme === 'dark') {
  isDark.value = true;
} else if (savedTheme === 'light') {
  isDark.value = false;
} else {
  isDark.value = false; // ou usar o sistema como fallback
}

// Atualiza DOM e salva sempre que `isDark` mudar
watchEffect(() => {
  const html = document.documentElement;
  if (isDark.value) {
    html.setAttribute('data-theme', 'dark');
    localStorage.setItem('theme-dashboard', 'dark');
  } else {
    html.setAttribute('data-theme', 'light');
    localStorage.setItem('theme-dashboard', 'light');
  }
});

// Alterna o tema
const toggleTheme = (): void => {
  isDark.value = !isDark.value;
};

// Alterna o drawer
const toggleDrawer = (): void => {
  const drawer = document.getElementById('my-drawer') as HTMLInputElement | null;
  if (drawer) {
    drawer.checked = !drawer.checked;
  }
};
</script>

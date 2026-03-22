<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="app-container">
    <aside class="sidebar">
      <div class="brand">
        <h2>⏱️ Timesheet</h2>
      </div>
      <nav>
        <RouterLink to="/" class="nav-link">Dashboard</RouterLink>
        <RouterLink to="/log-time" class="nav-link">Log Time</RouterLink>
        <RouterLink to="/history" class="nav-link">History</RouterLink>
      </nav>
    </aside>

    <main class="content">
      <RouterView />
    </main>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  min-height: 100vh;
}

.sidebar {
  width: 250px;
  background-color: var(--sidebar-bg);
  color: var(--sidebar-text);
  display: flex;
  flex-direction: column;
}

.brand {
  padding: 20px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.brand h2 {
  font-size: 1.25rem;
  font-weight: 600;
}

nav {
  padding: 20px 0;
  display: flex;
  flex-direction: column;
}

.nav-link {
  padding: 15px 20px;
  color: var(--sidebar-text);
  text-decoration: none;
  transition: background-color 0.2s;
}

.nav-link:hover, .router-link-active {
  background-color: rgba(255, 255, 255, 0.1);
  border-left: 4px solid var(--accent-color);
}

.content {
  flex: 1;
  padding: 40px;
  overflow-y: auto;
}
</style>

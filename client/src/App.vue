<template>
  <div class="shell">
    <aside class="sidebar">
      <div class="sidebar-logo">
        <h1>{{ t('nav.companyName') }}</h1>
        <span class="subtitle">{{ t('nav.subtitle') }}</span>
      </div>
      <nav class="sidebar-nav" aria-label="Main">
        <router-link to="/" class="nav-item" :class="{ active: $route.path === '/' }" :aria-current="$route.path === '/' ? 'page' : null">
          <svg class="nav-icon" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path d="M2 8L9 2L16 8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M4 7V15C4 15.5523 4.44772 16 5 16H13C13.5523 16 14 15.5523 14 15V7" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M7 16V11H11V16" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.overview') }}</span>
        </router-link>
        <router-link to="/inventory" class="nav-item" :class="{ active: $route.path === '/inventory' }" :aria-current="$route.path === '/inventory' ? 'page' : null">
          <svg class="nav-icon" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path d="M2 5.5L9 2L16 5.5L9 9L2 5.5Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M2 5.5V12.5L9 16L16 12.5V5.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M9 9V16" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.inventory') }}</span>
        </router-link>
        <router-link to="/orders" class="nav-item" :class="{ active: $route.path === '/orders' }" :aria-current="$route.path === '/orders' ? 'page' : null">
          <svg class="nav-icon" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path d="M6 3H12C12.5523 3 13 3.44772 13 4V15C13 15.5523 12.5523 16 12 16H6C5.44772 16 5 15.5523 5 15V4C5 3.44772 5.44772 3 6 3Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M7 2H11V4H7V2Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M7 8H11" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M7 11H11" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.orders') }}</span>
        </router-link>
        <router-link to="/spending" class="nav-item" :class="{ active: $route.path === '/spending' }" :aria-current="$route.path === '/spending' ? 'page' : null">
          <svg class="nav-icon" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <circle cx="9" cy="9" r="7" stroke="currentColor" stroke-width="1.5"/>
            <path d="M9 5V13" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M11.25 7C11.25 6.17157 10.2426 5.5 9 5.5C7.75736 5.5 6.75 6.17157 6.75 7C6.75 7.82843 7.75736 8.5 9 8.5C10.2426 8.5 11.25 9.17157 11.25 10C11.25 10.8284 10.2426 11.5 9 11.5C7.75736 11.5 6.75 10.8284 6.75 10" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.finance') }}</span>
        </router-link>
        <router-link to="/demand" class="nav-item" :class="{ active: $route.path === '/demand' }" :aria-current="$route.path === '/demand' ? 'page' : null">
          <svg class="nav-icon" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path d="M2 13L6.5 8L10 11L16 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M11.5 4H16V8.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.demandForecast') }}</span>
        </router-link>
        <router-link to="/reports" class="nav-item" :class="{ active: $route.path === '/reports' }" :aria-current="$route.path === '/reports' ? 'page' : null">
          <svg class="nav-icon" width="18" height="18" viewBox="0 0 18 18" fill="none">
            <path d="M4 2H11L15 6V15C15 15.5523 14.5523 16 14 16H4C3.44772 16 3 15.5523 3 15V3C3 2.44772 3.44772 2 4 2Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M6.5 12.5V10" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M9 12.5V8.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            <path d="M11.5 12.5V11" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">Reports</span>
        </router-link>
      </nav>
      <div class="sidebar-footer">
        <LanguageSwitcher />
        <ProfileMenu
          @show-profile-details="showProfileDetails = true"
          @show-tasks="showTasks = true"
        />
      </div>
    </aside>
    <div class="main-shell">
      <FilterBar />
      <main class="main-content">
        <router-view />
      </main>
    </div>

    <ProfileDetailsModal
      :is-open="showProfileDetails"
      @close="showProfileDetails = false"
    />

    <TasksModal
      :is-open="showTasks"
      :tasks="tasks"
      @close="showTasks = false"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-task="toggleTask"
    />
  </div>
</template>

<script>
import { ref, onMounted, computed } from 'vue'
import { api } from './api'
import { useAuth } from './composables/useAuth'
import { useI18n } from './composables/useI18n'
import FilterBar from './components/FilterBar.vue'
import ProfileMenu from './components/ProfileMenu.vue'
import ProfileDetailsModal from './components/ProfileDetailsModal.vue'
import TasksModal from './components/TasksModal.vue'
import LanguageSwitcher from './components/LanguageSwitcher.vue'

export default {
  name: 'App',
  components: {
    FilterBar,
    ProfileMenu,
    ProfileDetailsModal,
    TasksModal,
    LanguageSwitcher
  },
  setup() {
    const { currentUser } = useAuth()
    const { t } = useI18n()
    const showProfileDetails = ref(false)
    const showTasks = ref(false)
    const apiTasks = ref([])

    // Merge mock tasks from currentUser with API tasks
    const tasks = computed(() => {
      return [...currentUser.value.tasks, ...apiTasks.value]
    })

    const loadTasks = async () => {
      try {
        apiTasks.value = await api.getTasks()
      } catch (err) {
        console.error('Failed to load tasks:', err)
      }
    }

    const addTask = async (taskData) => {
      try {
        const newTask = await api.createTask(taskData)
        // Add new task to the beginning of the array
        apiTasks.value.unshift(newTask)
      } catch (err) {
        console.error('Failed to add task:', err)
      }
    }

    const deleteTask = async (taskId) => {
      try {
        // Check if it's a mock task (from currentUser)
        const isMockTask = currentUser.value.tasks.some(t => t.id === taskId)

        if (isMockTask) {
          // Remove from mock tasks
          const index = currentUser.value.tasks.findIndex(t => t.id === taskId)
          if (index !== -1) {
            currentUser.value.tasks.splice(index, 1)
          }
        } else {
          // Remove from API tasks
          await api.deleteTask(taskId)
          apiTasks.value = apiTasks.value.filter(t => t.id !== taskId)
        }
      } catch (err) {
        console.error('Failed to delete task:', err)
      }
    }

    const toggleTask = async (taskId) => {
      try {
        // Check if it's a mock task (from currentUser)
        const mockTask = currentUser.value.tasks.find(t => t.id === taskId)

        if (mockTask) {
          // Toggle mock task status
          mockTask.status = mockTask.status === 'pending' ? 'completed' : 'pending'
        } else {
          // Toggle API task
          const updatedTask = await api.toggleTask(taskId)
          const index = apiTasks.value.findIndex(t => t.id === taskId)
          if (index !== -1) {
            apiTasks.value[index] = updatedTask
          }
        }
      } catch (err) {
        console.error('Failed to toggle task:', err)
      }
    }

    onMounted(loadTasks)

    return {
      t,
      showProfileDetails,
      showTasks,
      tasks,
      addTask,
      deleteTask,
      toggleTask
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  background: #f8fafc;
  color: #1e293b;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.shell {
  display: grid;
  grid-template-columns: 260px 1fr;
  min-height: 100vh;
}

.sidebar {
  position: sticky;
  top: 0;
  height: 100vh;
  overflow: visible;
  background: #ffffff;
  border-right: 1px solid #e2e8f0;
  display: flex;
  flex-direction: column;
  z-index: 100;
}

.sidebar-logo {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 1.5rem 1.25rem;
  border-bottom: 1px solid #e2e8f0;
}

.sidebar-logo h1 {
  font-size: 1.25rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.subtitle {
  font-size: 0.813rem;
  color: #64748b;
  font-weight: 400;
}

.sidebar-nav {
  flex: 1;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 1rem 0.75rem;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  padding: 0.625rem 1rem;
  color: #64748b;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.938rem;
  border-radius: 6px;
  border-left: 3px solid transparent;
  transition: all 0.2s ease;
  position: relative;
}

.nav-icon {
  flex-shrink: 0;
}

.nav-item:hover {
  color: #0f172a;
  background: #f1f5f9;
}

.nav-item.active {
  color: #2563eb;
  background: #eff6ff;
  border-left-color: #2563eb;
}

.sidebar-footer {
  border-top: 1px solid #e2e8f0;
  padding: 1rem 0.75rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  overflow: visible;
}

.sidebar-footer .language-switcher,
.sidebar-footer .profile-menu {
  width: 100%;
}

.sidebar-footer .language-button,
.sidebar-footer .profile-button {
  width: 100%;
  justify-content: flex-start;
}

.sidebar-footer .profile-name {
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.main-shell {
  display: flex;
  flex-direction: column;
  min-width: 0;
}

.main-content {
  flex: 1;
  width: 100%;
  padding: 1.5rem 2rem;
}

.page-header {
  margin-bottom: 1.5rem;
}

.page-header h2 {
  font-size: 1.875rem;
  font-weight: 700;
  color: #0f172a;
  margin-bottom: 0.375rem;
  letter-spacing: -0.025em;
}

.page-header p {
  color: #64748b;
  font-size: 0.938rem;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.25rem;
  margin-bottom: 1.5rem;
}

.stat-card {
  background: white;
  padding: 1.25rem;
  border-radius: 10px;
  border: 1px solid #e2e8f0;
  transition: all 0.2s ease;
}

.stat-card:hover {
  border-color: #cbd5e1;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
}

.stat-label {
  color: #64748b;
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 0.625rem;
}

.stat-value {
  font-size: 2.25rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.stat-card.warning .stat-value {
  color: #ea580c;
}

.stat-card.success .stat-value {
  color: #059669;
}

.stat-card.danger .stat-value {
  color: #dc2626;
}

.stat-card.info .stat-value {
  color: #2563eb;
}

.card {
  background: white;
  border-radius: 10px;
  padding: 1.25rem;
  border: 1px solid #e2e8f0;
  margin-bottom: 1.25rem;
  transition: all 0.2s ease;
}

.card:hover {
  border-color: #cbd5e1;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 0.875rem;
  border-bottom: 1px solid #e2e8f0;
}

.card-title {
  font-size: 1.125rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.table-container {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
  border-bottom: 1px solid #e2e8f0;
}

th {
  text-align: left;
  padding: 0.5rem 0.75rem;
  font-weight: 600;
  color: #475569;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

td {
  padding: 0.5rem 0.75rem;
  border-top: 1px solid #f1f5f9;
  color: #334155;
  font-size: 0.875rem;
}

tbody tr {
  transition: background-color 0.15s ease;
}

tbody tr:hover {
  background: #f8fafc;
}

.badge {
  display: inline-block;
  padding: 0.313rem 0.75rem;
  border-radius: 6px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.025em;
}

.badge.success {
  background: #d1fae5;
  color: #065f46;
}

.badge.warning {
  background: #fed7aa;
  color: #92400e;
}

.badge.danger {
  background: #fecaca;
  color: #991b1b;
}

.badge.info {
  background: #dbeafe;
  color: #1e40af;
}

.badge.increasing {
  background: #d1fae5;
  color: #065f46;
}

.badge.decreasing {
  background: #fecaca;
  color: #991b1b;
}

.badge.stable {
  background: #e0e7ff;
  color: #3730a3;
}

.badge.high {
  background: #fecaca;
  color: #991b1b;
}

.badge.medium {
  background: #fed7aa;
  color: #92400e;
}

.badge.low {
  background: #dbeafe;
  color: #1e40af;
}

.loading {
  text-align: center;
  padding: 3rem;
  color: #64748b;
  font-size: 0.938rem;
}

.error {
  background: #fef2f2;
  border: 1px solid #fecaca;
  color: #991b1b;
  padding: 1rem;
  border-radius: 8px;
  margin: 1rem 0;
  font-size: 0.938rem;
}

@media (max-width: 900px) {
  .shell {
    grid-template-columns: 72px 1fr;
  }

  .sidebar-logo h1,
  .sidebar-logo .subtitle {
    display: none;
  }

  .sidebar-logo {
    padding: 1.25rem 0.5rem;
    align-items: center;
  }

  .sidebar-nav {
    padding: 1rem 0.625rem;
    align-items: center;
  }

  .nav-item {
    justify-content: center;
    padding: 0.625rem;
    width: 100%;
  }

  .nav-label {
    display: none;
  }

  .sidebar-footer {
    padding: 1rem 0.5rem;
    align-items: center;
  }

  .sidebar-footer .language-button,
  .sidebar-footer .profile-button {
    justify-content: center;
    padding: 0.5rem;
  }

  .sidebar-footer .language-label,
  .sidebar-footer .profile-name,
  .sidebar-footer .chevron {
    display: none;
  }

  .main-content {
    padding: 1.25rem 1rem;
  }
}
</style>

<template>
  <div class="page">
    <header class="header">
      <div class="container header-inner">
        <div class="logo">CSUCC Dashboard</div>
        <nav class="nav">
          <span class="user-name">Welcome, {{ user?.name }}</span>
          <button @click="logout" class="btn-outline">Logout</button>
        </nav>
      </div>
    </header>

    <main class="main-content">
      <section class="dashboard-content container">
        <h1>Dashboard</h1>
        <p>You have successfully logged in.</p>
        <div class="card">
          <p><strong>Name:</strong> {{ user?.name }}</p>
          <p><strong>Email:</strong> {{ user?.email }}</p>
        </div>
      </section>
    </main>

    <footer class="footer">
      <div class="container">
        <p>All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const user = ref(null)

onMounted(() => {
  const userData = localStorage.getItem('user')
  if (!userData) {
    router.push('/login')
  } else {
    user.value = JSON.parse(userData)
  }
})

function logout() {
  localStorage.removeItem('token')
  localStorage.removeItem('user')
  router.push('/')
}
</script>

<style scoped>
* { box-sizing: border-box; margin: 0; padding: 0; }

.page {
  font-family: Arial, sans-serif;
  font-size: 15px;
  color: #222;
  background: #fff;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.container {
  max-width: 900px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Header */
.header {
  background: #1a4a8a;
  color: #fff;
  padding: 12px 0;
}
.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.logo {
  font-size: 20px;
  font-weight: bold;
  color: #fff;
  letter-spacing: 1px;
}
.nav {
  display: flex;
  align-items: center;
  gap: 16px;
}
.user-name {
  color: #fff;
  font-size: 14px;
}

/* Buttons */
.btn-outline {
  background: #fff;
  color: #1a4a8a;
  padding: 7px 16px;
  border-radius: 4px;
  text-decoration: none;
  font-size: 14px;
  border: 1px solid #1a4a8a;
  display: inline-block;
  cursor: pointer;
}
.btn-outline:hover { background: #f0f4ff; }

/* Main Content */
.main-content {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Dashboard Content */
.dashboard-content {
  padding: 60px 20px;
  text-align: center;
  width: 100%;
}
.dashboard-content h1 {
  font-size: 28px;
  margin-bottom: 12px;
  color: #1a4a8a;
}
.dashboard-content p {
  color: #555;
  margin-bottom: 24px;
}

.card {
  background: #fafafa;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 24px;
  max-width: 400px;
  margin: 0 auto;
  text-align: left;
}
.card p {
  margin-bottom: 12px;
  color: #333;
}
.card p:last-child {
  margin-bottom: 0;
}

/* Footer */
.footer {
  margin-top: auto;
  background: #f5f5f5;
  border-top: 1px solid #ddd;
  padding: 16px 0;
  text-align: center;
  font-size: 13px;
  color: #777;
}
</style>

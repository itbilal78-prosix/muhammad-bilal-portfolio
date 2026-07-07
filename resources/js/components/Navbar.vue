<template>
  <nav class="navbar navbar-expand-lg premium-navbar fixed-top">
    <div class="container nav-container">
      <router-link class="brand" to="/">
        <span class="brand-logo">MB</span>
        <span class="brand-text">
          Muhammad <b>Bilal</b>
          <small>Full Stack Developer</small>
        </span>
      </router-link>


      <button
        class="menu-btn navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarMenu"
      >
        <span></span><span></span><span></span>
      </button>

      <div id="navbarMenu" class="collapse navbar-collapse">
        <ul class="navbar-nav ms-auto nav-links">
          <li class="nav-item"><router-link class="nav-link" to="/">Home</router-link></li>
          <li class="nav-item"><router-link class="nav-link" to="/about">About</router-link></li>
          <li class="nav-item"><router-link class="nav-link" to="/skills">Skills</router-link></li>
          <li class="nav-item"><router-link class="nav-link" to="/projects">Projects</router-link></li>
          <li class="nav-item"><router-link class="nav-link" to="/contact">Contact</router-link></li>
        </ul>

        <div class="nav-actions">
           <button class="theme-btn" @click="toggleTheme" type="button">
        {{ theme === 'dark' ? '☀️' : '🌙' }}
      </button>

          <router-link to="/contact" class="hire-btn">Hire Me</router-link>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const theme = ref('dark')

const applyTheme = (value) => {
  theme.value = value
  document.documentElement.setAttribute('data-theme', value)
  localStorage.setItem('portfolio_theme', value)
}

const toggleTheme = () => {
  applyTheme(theme.value === 'dark' ? 'light' : 'dark')
}

onMounted(() => {
  const saved = localStorage.getItem('portfolio_theme') || 'dark'
  applyTheme(saved)
})
</script>

<style scoped>
.premium-navbar {
  padding: 14px 0;
  background: var(--nav-bg, rgba(8, 8, 8, 0.9));
  backdrop-filter: blur(18px);
  border-bottom: 1px solid rgba(212, 175, 55, 0.18);
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.18);
  z-index: 9999;
}

.nav-container {
  display: flex;
  align-items: center;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
  flex-shrink: 0;
}

.brand-logo {
  width: 45px;
  height: 45px;
  border-radius: 14px;
  background: linear-gradient(135deg, #8b6b18, #d4af37, #f5d76e);
  display: flex;
  align-items: center;
  justify-content: center;
  color: #111;
  font-size: 17px;
  font-weight: 900;
  box-shadow: 0 12px 34px rgba(212, 175, 55, 0.35);
}

.brand-text {
  color: var(--text-main, #f8f8f8);
  font-size: 18px;
  font-weight: 600;
  line-height: 1.1;
}

.brand-text b {
  color: #d4af37;
}

.brand-text small {
  display: block;
  margin-top: 4px;
  font-size: 11px;
  color: var(--text-muted, #a8a8a8);
  letter-spacing: 0.5px;
}

.nav-links {
  align-items: center;
  gap: 8px;
}

.nav-link {
  position: relative;
  color: var(--text-muted, #d0d0d0) !important;
  font-size: 15px;
  font-weight: 500;
  padding: 10px 12px !important;
  transition: 0.3s ease;
}

.nav-link:hover,
.nav-link.router-link-active,
.nav-link.router-link-exact-active {
  color: #d4af37 !important;
}

.nav-link::after {
  content: "";
  position: absolute;
  left: 12px;
  right: 12px;
  bottom: 4px;
  height: 2px;
  border-radius: 10px;
  background: linear-gradient(90deg, #8b6b18, #d4af37, #f5d76e);
  transform: scaleX(0);
  transform-origin: left;
  transition: 0.3s ease;
}

.nav-link:hover::after,
.nav-link.router-link-active::after,
.nav-link.router-link-exact-active::after {
  transform: scaleX(1);
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-left: 22px;
}

.resume-btn,
.hire-btn {
  text-decoration: none;
  border-radius: 999px;
  padding: 10px 18px;
  font-size: 14px;
  font-weight: 800;
  transition: 0.3s ease;
  white-space: nowrap;
}

.resume-btn {
  color: #d4af37;
  border: 1px solid rgba(212, 175, 55, 0.6);
  background: rgba(212, 175, 55, 0.05);
}

.resume-btn:hover {
  color: #111;
  background: #d4af37;
}

.hire-btn {
  color: #111;
  background: linear-gradient(135deg, #8b6b18, #d4af37, #f5d76e);
  box-shadow: 0 15px 40px rgba(212, 175, 55, 0.35);
}

.hire-btn:hover {
  color: #111;
  transform: translateY(-2px);
}

.theme-btn {
  margin-left: auto;
  margin-right: 12px;
  width: 42px;
  height: 42px;
  border-radius: 50%;
  border: 1px solid rgba(212, 175, 55, 0.35);
  background: rgba(212, 175, 55, 0.12);
  color: #d4af37;
  cursor: pointer;
}

.menu-btn {
  display: none;
  width: 44px;
  height: 40px;
  border: 1px solid rgba(212, 175, 55, 0.3);
  border-radius: 12px;
  background: rgba(212, 175, 55, 0.08);
  padding: 9px;
  box-shadow: none !important;
}

.menu-btn span {
  display: block;
  height: 2px;
  background: #d4af37;
  border-radius: 10px;
  margin: 5px 0;
}

@media (min-width: 992px) {
  #navbarMenu {
    display: flex !important;
  }
}

@media (max-width: 991px) {
  .nav-container {
    flex-wrap: wrap;
  }

  .menu-btn {
    display: block;
  }

  #navbarMenu {
    width: 100%;
  }

  .navbar-collapse {
    margin-top: 16px;
    padding: 18px;
    border-radius: 20px;
    background: var(--card-bg, rgba(12, 12, 12, 0.98));
    border: 1px solid rgba(212, 175, 55, 0.18);
  }

  .nav-actions {
    margin-left: 0;
    margin-top: 14px;
    flex-direction: column;
    align-items: stretch;
  }

  .resume-btn,
  .hire-btn {
    width: 100%;
    text-align: center;
  }
}
</style>

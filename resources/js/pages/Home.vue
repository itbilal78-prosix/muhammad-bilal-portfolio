<template>
  <div class="portfolio">
    <nav-component />

    <section class="hero" id="about">
      <canvas ref="trailCanvas" class="trail-canvas"></canvas>

      <div class="hero-bg">
        <span class="orb orb-1"></span>
        <span class="orb orb-2"></span>

        <span class="float-code code-1">Laravel</span>
        <span class="float-code code-2">Vue.js</span>
        <span class="float-code code-3">PHP</span>
        <span class="float-code code-4">MySQL</span>
        <span class="float-code code-5">Flutter</span>
        <span class="float-code code-6">REST API</span>
      </div>

      <div class="container hero-content">
        <div class="hero-eyebrow">Full-Stack Developer · Lahore, PK</div>

        <h1 class="hero-h1">
          I build production web apps
          <br />
          with <em>Laravel</em>, <em>Vue.js</em> &amp; <em>Flutter</em>.
        </h1>

        <p class="hero-desc">
          Full Stack Web & Mobile App Developer specializing in Laravel, Vue.js,
          Flutter, PHP, and WordPress. I build modern, scalable, and
          high-performance web applications and mobile apps with clean code,
          exceptional UI/UX, and solutions designed for real business growth.
        </p>

        <div class="hero-btns">
          <a href="#contact" class="btn-primary">Hire Me</a>
          <a href="#projects" class="btn-outline">View Work →</a>
          <a
            href="/Muhammad-Bilal-Resume.pdf"
            download="Muhammad-Bilal-Resume.pdf"
            class="btn-outline resume-btn"
          >
            ⬇ Download Resume
          </a>
        </div>

        <div class="stats-row">
          <div class="stat">
            <div class="num">2+</div>
            <div class="lbl">Years Exp</div>
          </div>
          <div class="stat">
            <div class="num">10+</div>
            <div class="lbl">Projects</div>
          </div>
          <div class="stat">
            <div class="num">Laravel · Vue</div>
            <div class="lbl">Core Stack</div>
          </div>
        </div>
      </div>
    </section>

    <div class="ticker-wrap">
      <div class="ticker-track">
        <span v-for="(skill, i) in tickerSkills" :key="i" class="ticker-item">
          <span class="tick-dot">✦</span>{{ skill }}
        </span>
      </div>
    </div>

    <section class="section services-section" id="services">
      <div class="container">
        <div class="section-head center">
          <div class="sec-label">What I Do</div>
          <h2 class="sec-title">Services I Deliver</h2>
          <p class="sec-sub powerful">
            From idea to deployment, I build secure, scalable, and modern digital
            solutions using Laravel, Vue.js, Flutter, and MySQL.
          </p>
        </div>

        <div class="services-grid">
          <div v-for="svc in services" :key="svc.num" class="svc-card">
            <div class="svc-icon">{{ svc.icon }}</div>
            <div class="svc-num">{{ svc.num }}</div>
            <div class="svc-name">{{ svc.name }}</div>
            <div class="svc-desc">{{ svc.desc }}</div>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="projects">
      <div class="container">
        <div class="sec-label">Work</div>
        <h2 class="sec-title">Selected Projects</h2>
        <p class="sec-sub">
          A sample of what I've shipped — from real-time customization tools
          to mobile applications.
        </p>

        <div class="projects-grid">
          <div v-for="proj in projects" :key="proj.name" class="proj-card">
            <div class="proj-header">
              <div class="proj-name">{{ proj.name }}</div>
              <a v-if="proj.link" :href="proj.link" target="_blank" class="proj-link">↗</a>
            </div>
            <div class="proj-desc">{{ proj.desc }}</div>
            <div class="proj-tags">
              <span v-for="tag in proj.tags" :key="tag" class="tag">{{ tag }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="experience">
      <div class="container">
        <div class="sec-label">Background</div>
        <h2 class="sec-title">Experience</h2>

        <div class="exp-list">
          <div v-for="exp in experiences" :key="exp.company" class="exp-item">
            <div class="exp-meta">
              <div class="exp-date">{{ exp.date }}</div>
              <div class="exp-location">{{ exp.location }}</div>
            </div>
            <div class="exp-body">
              <div class="exp-company">{{ exp.company }}</div>
              <div class="exp-role">{{ exp.role }}</div>
              <div class="exp-detail">{{ exp.detail }}</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section">
      <div class="container">
        <div class="sec-label">Skills</div>
        <h2 class="sec-title">Daily Toolkit</h2>

        <div class="skills-wrap">
          <div v-for="group in skillGroups" :key="group.label" class="skill-group">
            <div class="skill-group-label">{{ group.label }}</div>
            <div class="skill-chips">
              <span v-for="chip in group.chips" :key="chip" class="chip">{{ chip }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="contact">
      <div class="container">
        <div class="cta-box">
          <div class="avail-dot">
            <span class="dot-pulse"></span>
            Available for work
          </div>

          <h2>Have a project in mind?</h2>

          <p>
            Tell me what you're building. I'll reply within 24 hours
            with an honest scope, timeline, and fixed quote.
          </p>

          <div class="cta-actions">
            <a href="mailto:itbilal73@gmail.com" class="btn-primary">Start a Project</a>
            <a href="tel:03015825174" class="btn-outline">📞 0301-5825174</a>
          </div>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="container footer-inner">
        <span>© 2026 Muhammad Bilal — Full-Stack Developer</span>
        <span>Built with Laravel · Vue · Flutter</span>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const trailCanvas = ref(null)
let ctx = null
let particles = []
let animationId = null

const resizeCanvas = () => {
  const canvas = trailCanvas.value
  if (!canvas) return
  canvas.width = canvas.offsetWidth
  canvas.height = canvas.offsetHeight
}

const addParticles = (e) => {
  const canvas = trailCanvas.value
  if (!canvas) return

  const rect = canvas.getBoundingClientRect()
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top

  for (let i = 0; i < 3; i++) {
    particles.push({
      x,
      y,
      size: Math.random() * 2.2 + 0.8,
      speedX: (Math.random() - 0.5) * 2,
      speedY: (Math.random() - 0.5) * 2,
      life: 0.7,
    })
  }
}

const animateTrail = () => {
  const canvas = trailCanvas.value
  if (!canvas || !ctx) return

  ctx.clearRect(0, 0, canvas.width, canvas.height)

  particles.forEach((p, index) => {
    p.x += p.speedX
    p.y += p.speedY
    p.life -= 0.018

    ctx.beginPath()
    ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2)
    ctx.fillStyle = `rgba(245, 166, 35, ${p.life})`
    ctx.shadowBlur = 14
    ctx.shadowColor = '#f5a623'
    ctx.fill()

    if (p.life <= 0) particles.splice(index, 1)
  })

  animationId = requestAnimationFrame(animateTrail)
}

onMounted(() => {
  const canvas = trailCanvas.value
  if (!canvas) return

  ctx = canvas.getContext('2d')
  resizeCanvas()

  window.addEventListener('resize', resizeCanvas)
  canvas.addEventListener('mousemove', addParticles)

  animateTrail()
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeCanvas)
  if (trailCanvas.value) {
    trailCanvas.value.removeEventListener('mousemove', addParticles)
  }
  if (animationId) cancelAnimationFrame(animationId)
})

const tickerSkills = [
  'Laravel', 'Vue.js', 'PHP', 'MySQL', 'Tailwind CSS',
  'Flutter', 'Git', 'REST APIs', 'Bootstrap', 'WordPress',
  'SQLite', 'Figma',
  'Laravel', 'Vue.js', 'PHP', 'MySQL', 'Tailwind CSS',
  'Flutter', 'Git', 'REST APIs', 'Bootstrap', 'WordPress',
  'SQLite', 'Figma',
]

const services = [
  {
    num: '01',
    icon: '⚡',
    name: 'Enterprise Web Applications',
    desc: 'Scalable Laravel & Vue.js business applications, CRM systems, ERP solutions, dashboards and SaaS platforms.',
  },
  {
    num: '02',
    icon: '🔐',
    name: 'REST API Development',
    desc: 'Fast, secure and clean REST APIs with authentication, payment gateways and third-party integrations.',
  },
  {
    num: '03',
    icon: '🎨',
    name: 'Frontend Development',
    desc: 'Responsive, pixel-perfect interfaces using Vue.js, Tailwind CSS and Bootstrap with smooth user experience.',
  },
  {
    num: '04',
    icon: '📱',
    name: 'Mobile Applications',
    desc: 'Cross-platform Flutter applications connected with Laravel APIs, Firebase notifications and secure authentication.',
  },
  {
    num: '05',
    icon: '🚀',
    name: 'Performance Optimization',
    desc: 'Database optimization, caching, code refactoring and speed improvements for existing Laravel applications.',
  },
  {
    num: '06',
    icon: '🛠️',
    name: 'Maintenance & Support',
    desc: 'Long-term application support, bug fixing, feature enhancements and production deployment.',
  },
]

const projects = [
  {
    name: 'Blogmatic SEO',
    link: '#',
    desc: 'Full-stack blogging platform with auth, role-based access, and premium payments.',
    tags: ['Laravel', 'Vue.js', 'MySQL'],
  },
  {
    name: 'Pakistan Cooling Center',
    link: '#',
    desc: 'eCommerce platform with dynamic inventory, orders, and optimized frontend.',
    tags: ['Laravel', 'Vue.js', 'Tailwind'],
  },
  {
    name: 'Prosix Sports',
    link: '#',
    desc: 'Sportswear customization platform with real-time previews and live workflows.',
    tags: ['Laravel', 'Vue.js', 'Flutter'],
  },
  {
    name: 'Travel Agency Platform',
    link: '#',
    desc: 'Umrah and transport booking website with SEO and mobile-first design.',
    tags: ['WordPress', 'PHP', 'SEO'],
  },
  {
    name: 'CRM Prosix',
    link: '#',
    desc: 'Employee and order management system with role-based auth and workflows.',
    tags: ['Laravel', 'MySQL', 'Bootstrap'],
  },
  {
    name: 'Prosix Mobile App',
    link: null,
    desc: 'Workforce management app with task allocation, tracking, and notifications.',
    tags: ['Flutter', 'Laravel', 'Firebase'],
  },
]

const experiences = [
  {
    date: 'Jun 2026 — Present',
    location: 'Remote',
    company: 'Prosix',
    role: 'Full Stack Developer',
    detail: 'Building Laravel, Vue.js, and MySQL applications with REST APIs and responsive UI.',
  },
  {
    date: 'Jun 2025 — Jan 2026',
    location: 'Lahore',
    company: 'Technology Brainz',
    role: 'WordPress Developer',
    detail: 'Developed responsive WordPress websites with Elementor, custom themes, optimization and maintenance.',
  },
  {
    date: 'Aug 2023 — Jun 2025',
    location: 'Lahore',
    company: 'Intelliage Solutions',
    role: 'Laravel Developer',
    detail: 'Built Laravel applications, REST APIs, and improved security, stability, and performance.',
  },
]

const skillGroups = [
  {
    label: 'Backend',
    chips: ['PHP', 'Laravel', 'Livewire', 'REST API', 'OOP / MVC', 'Firebase FCM'],
  },
  {
    label: 'Frontend',
    chips: ['Vue.js', 'JavaScript', 'HTML5', 'CSS3', 'Tailwind CSS', 'Bootstrap'],
  },
  {
    label: 'Mobile & Database',
    chips: ['Flutter', 'MySQL', 'SQLite'],
  },
  {
    label: 'Tools',
    chips: ['Git', 'GitHub', 'Bitbucket', 'Figma', 'WordPress'],
  },
]
</script>

<style scoped>
:global(:root) {
  --bg-main: #0d1117;
  --bg-soft: #151a21;
  --card-bg: #161b22;
  --text-main: #e6edf3;
  --text-muted: #9aa4b2;
  --border: #2f3742;
  --gold: #f5a623;
  --gold-soft: rgba(245, 166, 35, 0.12);
  --nav-bg: rgba(13, 17, 23, 0.92);
}

:global(html[data-theme="light"]) {
  --bg-main: #f7f7f4;
  --bg-soft: #ffffff;
  --card-bg: #ffffff;
  --text-main: #111827;
  --text-muted: #5f6673;
  --border: #d8d8d8;
  --gold: #c88412;
  --gold-soft: rgba(200, 132, 18, 0.12);
  --nav-bg: rgba(255, 255, 255, 0.92);
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.portfolio {
  background: var(--bg-main);
  color: var(--text-main);
  font-family: 'Inter', system-ui, sans-serif;
  line-height: 1.6;
  min-height: 100vh;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 24px;
}

.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 140px 0 90px;
  overflow: hidden;
}

.trail-canvas {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  pointer-events: auto;
}

.hero-bg {
  position: absolute;
  inset: 0;
  overflow: hidden;
  z-index: 0;
  pointer-events: none;
  background:
    radial-gradient(circle at 18% 25%, rgba(245, 166, 35, 0.12), transparent 26%),
    radial-gradient(circle at 82% 30%, rgba(245, 166, 35, 0.08), transparent 28%),
    linear-gradient(180deg, rgba(255,255,255,0.025), transparent);
}

.hero-bg::before {
  content: "";
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.035) 1px, transparent 1px);
  background-size: 52px 52px;
  mask-image: radial-gradient(circle, #000 30%, transparent 78%);
}

.orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(55px);
  opacity: 0.22;
  animation: floatOrb 10s ease-in-out infinite;
}

.orb-1 {
  width: 260px;
  height: 260px;
  background: var(--gold);
  top: 16%;
  right: 12%;
}

.orb-2 {
  width: 220px;
  height: 220px;
  background: var(--gold);
  bottom: 18%;
  left: 10%;
  animation-delay: 2s;
}

@keyframes floatOrb {
  0%, 100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-24px) scale(1.05);
  }
}

.float-code {
  position: absolute;
  color: var(--gold);
  font-family: monospace;
  font-size: 13px;
  border: 1px solid rgba(245, 166, 35, 0.22);
  background: rgba(245, 166, 35, 0.07);
  padding: 7px 13px;
  border-radius: 999px;
  animation: floatCode 8s ease-in-out infinite;
  backdrop-filter: blur(8px);
}

.code-1 { top: 21%; right: 17%; }
.code-2 { top: 39%; right: 8%; animation-delay: 1s; }
.code-3 { bottom: 27%; right: 18%; animation-delay: 2s; }
.code-4 { top: 68%; left: 9%; animation-delay: 3s; }
.code-5 { top: 25%; left: 13%; animation-delay: 4s; }
.code-6 { bottom: 18%; left: 22%; animation-delay: 5s; }

@keyframes floatCode {
  0%, 100% {
    transform: translateY(0);
    opacity: 0.55;
  }
  50% {
    transform: translateY(-14px);
    opacity: 0.9;
  }
}

.hero-content {
  position: relative;
  z-index: 3;
  max-width: 930px;
  margin: auto;
  pointer-events: none;
}

.hero-content a {
  pointer-events: auto;
}

.hero-eyebrow {
  font-family: monospace;
  font-size: 12px;
  color: var(--gold);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 24px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.hero-eyebrow::before,
.hero-eyebrow::after {
  content: '';
  width: 32px;
  height: 1px;
  background: var(--gold);
}

.hero-h1 {
  font-size: clamp(36px, 4vw, 70px);
  font-weight: 800;
  line-height: 1.06;
  letter-spacing: -2px;
  margin-bottom: 24px;
}

.hero-h1 em {
  font-style: normal;
  color: var(--gold);
  text-shadow: 0 0 28px rgba(245, 166, 35, 0.18);
}

.hero-desc {
  font-size: clamp(15px, 2vw, 18px);
  color: var(--text-muted);
  max-width: 760px;
  line-height: 1.85;
  margin: 0 auto 38px;
}

.hero-btns {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
  justify-content: center;
  margin-bottom: 52px;
}

.btn-primary,
.btn-outline {
  font-size: 14px;
  font-weight: 800;
  padding: 13px 30px;
  border-radius: 10px;
  text-decoration: none;
  display: inline-block;
  transition: all 0.28s ease;
}

.btn-primary {
  background: var(--gold);
  color: #0d1117;
  border: 1.5px solid var(--gold);
  box-shadow: 0 12px 32px rgba(245, 166, 35, 0.18);
}

.btn-primary:hover {
  background: transparent;
  color: var(--gold);
  transform: translateY(-2px);
  box-shadow: 0 0 24px rgba(245, 166, 35, 0.28);
}

.btn-outline {
  background: rgba(255, 255, 255, 0.02);
  color: var(--text-main);
  border: 1.5px solid var(--border);
}

.btn-outline:hover {
  background: var(--gold);
  border-color: var(--gold);
  color: #0d1117;
  transform: translateY(-2px);
  box-shadow: 0 0 22px rgba(245, 166, 35, 0.22);
}

.resume-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.stats-row {
  display: flex;
  gap: 22px;
  flex-wrap: wrap;
  justify-content: center;
}

.stat {
  min-width: 150px;
  background: rgba(255,255,255,0.035);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 18px;
  text-align: left;
  transition: all 0.28s ease;
}

.stat:hover {
  border-color: rgba(245, 166, 35, 0.55);
  transform: translateY(-4px);
}

.stat .num {
  font-size: 26px;
  font-weight: 900;
  color: var(--text-main);
  line-height: 1;
}

.stat .lbl {
  font-size: 11px;
  color: var(--text-muted);
  margin-top: 8px;
  text-transform: uppercase;
  letter-spacing: 0.8px;
}

.ticker-wrap {
  border-top: 0.5px solid var(--border);
  border-bottom: 0.5px solid var(--border);
  padding: 14px 0;
  overflow: hidden;
}

.ticker-track {
  display: flex;
  gap: 48px;
  white-space: nowrap;
  animation: ticker 22s linear infinite;
}

.ticker-item {
  font-family: monospace;
  font-size: 13px;
  color: var(--text-muted);
  font-weight: 500;
  flex-shrink: 0;
}

.tick-dot {
  color: var(--gold);
  margin-right: 8px;
}

@keyframes ticker {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

.section {
  padding: 96px 0;
}

.services-section {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background:
    radial-gradient(circle at top left, rgba(245, 166, 35, 0.06), transparent 35%),
    linear-gradient(180deg, rgba(255,255,255,0.018), transparent);
}

.section-head.center {
  text-align: center;
  max-width: 820px;
  margin: 0 auto 54px;
}

.sec-label {
  font-family: monospace;
  font-size: 11px;
  color: var(--gold);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 10px;
}

.center .sec-label::before,
.center .sec-label::after {
  content: '—';
  margin: 0 10px;
  color: var(--gold);
}

.sec-title {
  font-size: clamp(30px, 4vw, 46px);
  font-weight: 900;
  letter-spacing: -1.2px;
  margin-bottom: 14px;
}

.sec-sub {
  font-size: 15px;
  color: var(--text-muted);
  max-width: 520px;
  line-height: 1.75;
  margin-bottom: 48px;
}

.sec-sub.powerful {
  max-width: 760px;
  margin: 0 auto;
  font-size: 17px;
  line-height: 1.9;
}

.services-grid,
.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}

.svc-card,
.proj-card,
.cta-box {
  background: linear-gradient(180deg, rgba(255,255,255,0.04), rgba(255,255,255,0.016));
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 26px;
  transition: all 0.28s ease;
}

.svc-card:hover,
.proj-card:hover {
  border-color: rgba(245, 166, 35, 0.55);
  transform: translateY(-5px);
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.22);
}

.svc-icon {
  width: 46px;
  height: 46px;
  border-radius: 14px;
  background: var(--gold-soft);
  color: var(--gold);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  margin-bottom: 22px;
}

.svc-num {
  font-family: monospace;
  font-size: 12px;
  color: var(--text-muted);
  margin-bottom: 8px;
}

.svc-name,
.proj-name {
  font-size: 18px;
  font-weight: 800;
  margin-bottom: 10px;
}

.svc-desc,
.proj-desc,
.exp-detail {
  font-size: 14px;
  color: var(--text-muted);
  line-height: 1.75;
}

.proj-header {
  display: flex;
  justify-content: space-between;
}

.proj-link {
  color: var(--text-muted);
  font-size: 16px;
  text-decoration: none;
}

.proj-link:hover {
  color: var(--gold);
}

.proj-tags {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-top: 12px;
}

.tag {
  background: rgba(245, 166, 35, 0.08);
  border: 1px solid rgba(245, 166, 35, 0.22);
  color: var(--gold);
  font-size: 11px;
  font-weight: 600;
  padding: 4px 10px;
  border-radius: 20px;
  font-family: monospace;
}

.exp-item {
  display: grid;
  grid-template-columns: 200px 1fr;
  gap: 32px;
  padding: 28px 0;
  border-bottom: 0.5px solid var(--border);
}

.exp-date,
.exp-location,
.exp-role,
.skill-group-label {
  font-family: monospace;
  font-size: 12px;
  color: var(--text-muted);
}

.exp-company {
  font-size: 15px;
  font-weight: 700;
}

.exp-role {
  color: var(--gold);
  margin-bottom: 10px;
}

.skills-wrap {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 32px;
}

.skill-group-label {
  letter-spacing: 1px;
  text-transform: uppercase;
  margin-bottom: 12px;
}

.skill-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.chip {
  background: var(--bg-soft);
  border: 0.5px solid var(--border);
  color: var(--text-main);
  font-size: 12px;
  font-weight: 500;
  padding: 6px 12px;
  border-radius: 6px;
}

.cta-box {
  padding: 64px 40px;
  text-align: center;
}

.cta-box h2 {
  font-size: clamp(22px, 4vw, 36px);
  font-weight: 800;
  margin-bottom: 12px;
}

.cta-box p {
  color: var(--text-muted);
  margin-bottom: 32px;
}

.avail-dot {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  color: var(--gold);
  font-family: monospace;
  margin-bottom: 20px;
}

.dot-pulse {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--gold);
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.35; }
}

.cta-actions {
  display: flex;
  gap: 14px;
  justify-content: center;
  flex-wrap: wrap;
}

.footer {
  border-top: 0.5px solid var(--border);
  padding: 28px 24px;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 8px;
  font-size: 12px;
  color: var(--text-muted);
  font-family: monospace;
}

@media (max-width: 991px) {
  .services-grid,
  .projects-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .hero-h1 {
    font-size: 44px;
  }
}

@media (max-width: 640px) {
  .hero {
    padding-top: 120px;
  }

  .hero-h1 {
    font-size: 34px;
  }

  .services-grid,
  .projects-grid {
    grid-template-columns: 1fr;
  }

  .exp-item {
    grid-template-columns: 1fr;
    gap: 8px;
  }

  .cta-box {
    padding: 40px 24px;
  }

  .footer-inner {
    flex-direction: column;
    text-align: center;
  }

  .float-code {
    display: none;
  }
}
</style>

<template>
  <div class="skills-page">
    <nav-component />

    <!-- HERO -->
    <section
      ref="heroSection"
      class="skills-hero"
      :style="heroVariables"
      @mousemove="handleHeroMouseMove"
      @mouseleave="resetHero"
    >
      <canvas ref="trailCanvas" class="trail-canvas"></canvas>

      <div class="hero-visual-bg">
        <div class="grid-layer"></div>
        <div class="cursor-light"></div>
        <div class="ambient ambient-one"></div>
        <div class="ambient ambient-two"></div>

        <span
          v-for="particle in decorativeParticles"
          :key="particle.id"
          class="decorative-particle"
          :style="particle.style"
        ></span>
      </div>

      <div class="container hero-grid">
        <div class="hero-copy" :style="copyTransform">
          <div class="section-label">Technical Skills</div>

          <h1>
            I turn technology into
            <span>reliable digital products.</span>
          </h1>

          <p class="hero-description">
            Laravel, Vue.js, Flutter, MySQL, APIs, deployment, and clean
            architecture — combined to build fast, secure, and scalable
            applications for real businesses.
          </p>

          <div class="hero-actions">
            <a href="#core-skills" class="btn-primary">
              Explore My Skills
            </a>

            <a href="#skills-contact" class="btn-outline">
              Work With Me
            </a>
          </div>

          <div class="hero-stats">
            <article v-for="item in stats" :key="item.label">
              <strong>{{ item.value }}</strong>
              <span>{{ item.label }}</span>
            </article>
          </div>
        </div>

        <!-- INTERACTIVE SKILL CONSTELLATION -->
        <div class="visual-column">
          <div
            class="skill-constellation"
            :style="constellationTransform"
          >
            <div class="constellation-glow"></div>

            <svg
              class="constellation-lines"
              viewBox="0 0 600 600"
              aria-hidden="true"
            >
              <line x1="300" y1="300" x2="300" y2="75" />
              <line x1="300" y1="300" x2="500" y2="175" />
              <line x1="300" y1="300" x2="505" y2="420" />
              <line x1="300" y1="300" x2="300" y2="535" />
              <line x1="300" y1="300" x2="95" y2="420" />
              <line x1="300" y1="300" x2="100" y2="175" />
              <circle cx="300" cy="300" r="205" />
              <circle cx="300" cy="300" r="135" />
            </svg>

            <div class="constellation-core">
              <span>Full Stack</span>
              <strong>MB</strong>
              <small>Developer</small>
            </div>

            <button
              v-for="skill in orbitSkills"
              :key="skill.name"
              type="button"
              class="skill-node"
              :class="skill.className"
              :style="getNodeTransform(skill)"
              @mousemove.stop="handleNodeMove($event, skill.name)"
              @mouseleave="resetNode(skill.name)"
            >
              <span>{{ skill.icon }}</span>
              <div>
                <strong>{{ skill.name }}</strong>
                <small>{{ skill.type }}</small>
              </div>
            </button>

            <!-- <div class="floating-terminal">
              <div class="terminal-head">
                <span></span><span></span><span></span>
                <small>stack.json</small>
              </div>

              <div class="terminal-code">
                <p><b>{</b></p>
                <p>&nbsp;&nbsp;<em>"backend"</em>: "Laravel",</p>
                <p>&nbsp;&nbsp;<em>"frontend"</em>: "Vue.js",</p>
                <p>&nbsp;&nbsp;<em>"mobile"</em>: "Flutter",</p>
                <p>&nbsp;&nbsp;<em>"database"</em>: "MySQL"</p>
                <p><b>}</b></p>
              </div>
            </div> -->
          </div>
        </div>
      </div>

      <div class="scroll-hint">
        <span>Scroll to explore</span>
        <i></i>
      </div>
    </section>

    <!-- TICKER -->
    <section class="skills-ticker">
      <div class="ticker-track">
        <span
          v-for="(skill, index) in tickerSkills"
          :key="`${skill}-${index}`"
        >
          <b>✦</b>{{ skill }}
        </span>
      </div>
    </section>

    <!-- CORE SKILLS -->
    <section id="core-skills" class="section">
      <div class="container">
        <div class="section-heading">
          <div>
            <div class="section-label">Core Expertise</div>
            <h2>A complete stack for modern applications.</h2>
          </div>

          <p>
            I manage the complete development workflow — planning, database
            design, backend development, responsive frontend, mobile apps,
            testing, deployment, and long-term maintenance.
          </p>
        </div>

        <div class="expertise-grid">
          <article
            v-for="(category, index) in skillCategories"
            :key="category.title"
            class="expertise-card"
          >
            <div class="expertise-top">
              <span class="expertise-icon">{{ category.icon }}</span>
              <span class="expertise-number">
                {{ String(index + 1).padStart(2, '0') }}
              </span>
            </div>

            <h3>{{ category.title }}</h3>
            <p>{{ category.description }}</p>

            <div class="skill-tags">
              <span v-for="skill in category.skills" :key="skill">
                {{ skill }}
              </span>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- PROFICIENCY -->
    <section class="section proficiency-section">
      <div class="container proficiency-grid">
        <div class="proficiency-copy">
          <div class="section-label">Practical Proficiency</div>
          <h2>Skills improved through real production work.</h2>

          <p>
            These levels represent practical experience from building business
            systems, APIs, dashboards, mobile applications, real-time features,
            and production deployments.
          </p>

          <div class="experience-note">
            <span>✦</span>
            <p>
              I focus on maintainable architecture, clean code, performance,
              security, and solutions that remain easy to extend.
            </p>
          </div>
        </div>

        <div class="progress-panel">
          <div
            v-for="skill in proficiencySkills"
            :key="skill.name"
            class="progress-item"
          >
            <div class="progress-header">
              <div>
                <span>{{ skill.icon }}</span>
                <strong>{{ skill.name }}</strong>
              </div>

              <b>{{ skill.level }}%</b>
            </div>

            <div class="progress-track">
              <span :style="{ width: `${skill.level}%` }"></span>
            </div>

            <p>{{ skill.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- DAILY TOOLKIT -->
    <section class="section">
      <div class="container">
        <div class="center-heading">
          <div class="section-label">Daily Toolkit</div>
          <h2>Technologies I use throughout development.</h2>
          <p>
            A balanced collection of frameworks, languages, databases,
            deployment tools, and collaboration software.
          </p>
        </div>

        <div class="tool-grid">
          <article
            v-for="tool in technologies"
            :key="tool.name"
            class="tool-card"
          >
            <span class="tool-icon">{{ tool.icon }}</span>

            <div>
              <h3>{{ tool.name }}</h3>
              <p>{{ tool.category }}</p>
            </div>

            <small>
              <i></i>
              Active
            </small>
          </article>
        </div>
      </div>
    </section>

    <!-- WORKFLOW -->
    <section class="section workflow-section">
      <div class="container">
        <div class="section-heading">
          <div>
            <div class="section-label">Development Workflow</div>
            <h2>From idea to stable production release.</h2>
          </div>

          <p>
            Every project follows a clear process so development stays
            organized, requirements remain visible, and the final product is
            easier to test and maintain.
          </p>
        </div>

        <div class="workflow-grid">
          <article
            v-for="(step, index) in workflowSteps"
            :key="step.title"
            class="workflow-card"
          >
            <span class="workflow-number">
              {{ String(index + 1).padStart(2, '0') }}
            </span>

            <span class="workflow-icon">{{ step.icon }}</span>
            <h3>{{ step.title }}</h3>
            <p>{{ step.description }}</p>
          </article>
        </div>
      </div>
    </section>

    <!-- STRENGTHS -->
    <section class="section">
      <div class="container">
        <div class="center-heading">
          <div class="section-label">Professional Strengths</div>
          <h2>Good software requires more than syntax.</h2>
          <p>
            Planning, communication, debugging, and business understanding are
            equally important for delivering a successful product.
          </p>
        </div>

        <div class="strength-grid">
          <article
            v-for="strength in strengths"
            :key="strength.title"
            class="strength-card"
          >
            <span>{{ strength.icon }}</span>
            <h3>{{ strength.title }}</h3>
            <p>{{ strength.description }}</p>
          </article>
        </div>
      </div>
    </section>

    <!-- CTA -->
    <section id="skills-contact" class="section contact-section">
      <div class="container">
        <div class="contact-box">
          <div class="contact-glow"></div>

          <div class="availability">
            <span></span>
            Available for new projects
          </div>

          <h2>Need these skills for your next product?</h2>

          <p>
            Let’s discuss your website, CRM, dashboard, REST API, automation,
            or mobile application and build a reliable solution.
          </p>

          <div class="contact-actions">
            <a href="mailto:itbilal73@gmail.com" class="btn-primary">
              Start a Project
            </a>

            <a href="tel:03015825174" class="btn-outline">
              Call: 0301-5825174
            </a>
          </div>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="container footer-inner">
        <span>© 2026 Muhammad Bilal — Full-Stack Developer</span>
        <span>Laravel · Vue.js · Flutter · MySQL</span>
      </div>
    </footer>
  </div>
</template>

<script setup>
import {
  computed,
  nextTick,
  onBeforeUnmount,
  onMounted,
  reactive,
  ref,
} from 'vue'

const heroSection = ref(null)
const trailCanvas = ref(null)

const pointer = reactive({
  x: 50,
  y: 50,
  normalizedX: 0,
  normalizedY: 0,
  active: false,
})

const nodeOffsets = reactive({})

let canvasContext = null
let canvasFrame = null
let particles = []
let lastParticleTime = 0

const heroVariables = computed(() => ({
  '--pointer-x': `${pointer.x}%`,
  '--pointer-y': `${pointer.y}%`,
  '--pointer-normal-x': pointer.normalizedX,
  '--pointer-normal-y': pointer.normalizedY,
}))

const copyTransform = computed(() => ({
  transform: `
    perspective(1200px)
    translate3d(
      ${pointer.normalizedX * -10}px,
      ${pointer.normalizedY * -8}px,
      0
    )
  `,
}))

const constellationTransform = computed(() => ({
  transform: `
    perspective(1200px)
    rotateX(${pointer.normalizedY * -7}deg)
    rotateY(${pointer.normalizedX * 8}deg)
    translate3d(
      ${pointer.normalizedX * 12}px,
      ${pointer.normalizedY * 10}px,
      0
    )
  `,
}))

const decorativeParticles = [
  { id: 1, style: { left: '8%', top: '24%', animationDelay: '0s' } },
  { id: 2, style: { left: '18%', top: '78%', animationDelay: '1.2s' } },
  { id: 3, style: { left: '77%', top: '14%', animationDelay: '2.1s' } },
  { id: 4, style: { left: '91%', top: '68%', animationDelay: '3.2s' } },
  { id: 5, style: { left: '64%', top: '84%', animationDelay: '4.1s' } },
]

const orbitSkills = [
  {
    name: 'Laravel',
    type: 'Backend',
    icon: 'L',
    className: 'node-laravel',
  },
  {
    name: 'Vue.js',
    type: 'Frontend',
    icon: 'V',
    className: 'node-vue',
  },
  {
    name: 'Flutter',
    type: 'Mobile',
    icon: 'F',
    className: 'node-flutter',
  },
  {
    name: 'MySQL',
    type: 'Database',
    icon: 'M',
    className: 'node-mysql',
  },
  {
    name: 'PHP',
    type: 'Language',
    icon: 'P',
    className: 'node-php',
  },
  {
    name: 'Git',
    type: 'Workflow',
    icon: 'G',
    className: 'node-git',
  },
]

const getNodeTransform = (skill) => {
  const offset = nodeOffsets[skill.name] || { x: 0, y: 0 }

  return {
    transform: `
      translate3d(
        ${offset.x + pointer.normalizedX * (skill.name.length % 2 ? 6 : -6)}px,
        ${offset.y + pointer.normalizedY * (skill.name.length % 2 ? -5 : 5)}px,
        28px
      )
    `,
  }
}

const handleNodeMove = (event, name) => {
  const node = event.currentTarget
  const rect = node.getBoundingClientRect()

  nodeOffsets[name] = {
    x: (event.clientX - rect.left - rect.width / 2) * 0.14,
    y: (event.clientY - rect.top - rect.height / 2) * 0.18,
  }
}

const resetNode = (name) => {
  nodeOffsets[name] = { x: 0, y: 0 }
}

const resizeCanvas = () => {
  const canvas = trailCanvas.value

  if (!canvas) return

  const rect = canvas.getBoundingClientRect()
  const ratio = window.devicePixelRatio || 1

  canvas.width = Math.round(rect.width * ratio)
  canvas.height = Math.round(rect.height * ratio)
  canvas.style.width = `${rect.width}px`
  canvas.style.height = `${rect.height}px`

  canvasContext = canvas.getContext('2d')

  if (canvasContext) {
    canvasContext.setTransform(ratio, 0, 0, ratio, 0, 0)
  }
}

const addParticles = (x, y) => {
  const now = performance.now()

  if (now - lastParticleTime < 17) return
  lastParticleTime = now

  for (let index = 0; index < 4; index += 1) {
    const angle = Math.random() * Math.PI * 2
    const speed = Math.random() * 1.4 + 0.35

    particles.push({
      x: x + (Math.random() - 0.5) * 8,
      y: y + (Math.random() - 0.5) * 8,
      vx: Math.cos(angle) * speed,
      vy: Math.sin(angle) * speed,
      size: Math.random() * 2.1 + 0.7,
      life: 1,
      opacity: Math.random() * 0.35 + 0.45,
    })
  }

  if (particles.length > 130) {
    particles = particles.slice(-130)
  }
}

const handleHeroMouseMove = (event) => {
  const section = heroSection.value

  if (!section) return

  const rect = section.getBoundingClientRect()
  const x = event.clientX - rect.left
  const y = event.clientY - rect.top

  pointer.x = (x / rect.width) * 100
  pointer.y = (y / rect.height) * 100
  pointer.normalizedX = x / rect.width - 0.5
  pointer.normalizedY = y / rect.height - 0.5
  pointer.active = true

  addParticles(x, y)
}

const resetHero = () => {
  pointer.x = 50
  pointer.y = 50
  pointer.normalizedX = 0
  pointer.normalizedY = 0
  pointer.active = false
}

const getThemeGold = () => {
  const value = getComputedStyle(document.documentElement)
    .getPropertyValue('--gold')
    .trim()

  return value || '#f5a623'
}

const animateParticles = () => {
  const canvas = trailCanvas.value

  if (!canvas || !canvasContext) {
    canvasFrame = requestAnimationFrame(animateParticles)
    return
  }

  const rect = canvas.getBoundingClientRect()
  const gold = getThemeGold()

  canvasContext.clearRect(0, 0, rect.width, rect.height)

  particles.forEach((particle) => {
    particle.x += particle.vx
    particle.y += particle.vy
    particle.vy += 0.002
    particle.life -= 0.022
    particle.size *= 0.992

    canvasContext.beginPath()
    canvasContext.arc(
      particle.x,
      particle.y,
      Math.max(particle.size, 0.2),
      0,
      Math.PI * 2,
    )

    canvasContext.fillStyle = gold
    canvasContext.globalAlpha = Math.max(
      particle.opacity * particle.life,
      0,
    )
    canvasContext.shadowBlur = 13
    canvasContext.shadowColor = gold
    canvasContext.fill()
  })

  canvasContext.globalAlpha = 1

  particles = particles.filter((particle) => particle.life > 0)
  canvasFrame = requestAnimationFrame(animateParticles)
}

onMounted(async () => {
  await nextTick()
  resizeCanvas()
  window.addEventListener('resize', resizeCanvas)
  canvasFrame = requestAnimationFrame(animateParticles)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeCanvas)

  if (canvasFrame) {
    cancelAnimationFrame(canvasFrame)
  }

  particles = []
})

const stats = [
  { value: '6+', label: 'Core Technologies' },
  { value: '10+', label: 'Projects Built' },
  { value: '2+', label: 'Years Experience' },
]

const tickerSkills = [
  'Laravel',
  'Vue.js',
  'PHP',
  'MySQL',
  'Flutter',
  'JavaScript',
  'REST API',
  'Firebase',
  'Bootstrap',
  'Tailwind CSS',
  'Git',
  'Ubuntu',
  'Laravel',
  'Vue.js',
  'PHP',
  'MySQL',
  'Flutter',
  'JavaScript',
  'REST API',
  'Firebase',
  'Bootstrap',
  'Tailwind CSS',
  'Git',
  'Ubuntu',
]

const skillCategories = [
  {
    icon: '⚙',
    title: 'Backend Development',
    description:
      'Secure business logic, authentication, APIs, background jobs, and scalable server-side applications.',
    skills: [
      'PHP',
      'Laravel',
      'Livewire',
      'REST API',
      'Sanctum',
      'Queues',
      'OOP',
      'MVC',
    ],
  },
  {
    icon: '◫',
    title: 'Frontend Development',
    description:
      'Responsive and interactive interfaces built for modern browsers and multiple screen sizes.',
    skills: [
      'Vue.js',
      'JavaScript',
      'HTML5',
      'CSS3',
      'Bootstrap',
      'Tailwind CSS',
      'Vite',
    ],
  },
  {
    icon: '▣',
    title: 'Mobile Development',
    description:
      'Cross-platform Flutter applications connected with Laravel APIs and Firebase services.',
    skills: [
      'Flutter',
      'Dart',
      'Firebase',
      'FCM',
      'Local Notifications',
      'API Integration',
    ],
  },
  {
    icon: '◉',
    title: 'Database Development',
    description:
      'Database design, relationships, migrations, reporting queries, and performance improvements.',
    skills: [
      'MySQL',
      'SQLite',
      'Eloquent ORM',
      'Indexes',
      'Relationships',
      'Query Optimization',
    ],
  },
  {
    icon: '⌘',
    title: 'Tools & Version Control',
    description:
      'Professional workflow using version control, package managers, debugging, and collaboration tools.',
    skills: [
      'Git',
      'GitHub',
      'Bitbucket',
      'Composer',
      'NPM',
      'Postman',
      'VS Code',
      'Figma',
    ],
  },
  {
    icon: '↗',
    title: 'Deployment & Production',
    description:
      'Production deployment, web server configuration, SSL, queues, cron jobs, and maintenance.',
    skills: [
      'Ubuntu',
      'Nginx',
      'SSL',
      'Cron Jobs',
      'Queue Workers',
      'Laravel Reverb',
      'Vercel',
    ],
  },
]

const proficiencySkills = [
  {
    icon: 'L',
    name: 'Laravel & PHP',
    level: 92,
    description:
      'Business applications, APIs, authentication, queues, notifications, and backend architecture.',
  },
  {
    icon: 'V',
    name: 'Vue.js & JavaScript',
    level: 86,
    description:
      'Dashboards, reusable components, API integrations, responsive interfaces, and SPA development.',
  },
  {
    icon: 'M',
    name: 'MySQL & Database Design',
    level: 88,
    description:
      'Relational design, Eloquent relationships, migrations, reporting, and query optimization.',
  },
  {
    icon: 'F',
    name: 'Flutter Development',
    level: 78,
    description:
      'Cross-platform applications, Laravel API integration, Firebase, and mobile notifications.',
  },
  {
    icon: 'U',
    name: 'Server & Deployment',
    level: 80,
    description:
      'Ubuntu, Nginx, SSL, production builds, queues, cron jobs, Git deployment, and maintenance.',
  },
]

const technologies = [
  { icon: 'L', name: 'Laravel', category: 'Backend Framework' },
  { icon: 'P', name: 'PHP', category: 'Backend Language' },
  { icon: 'V', name: 'Vue.js', category: 'Frontend Framework' },
  { icon: 'J', name: 'JavaScript', category: 'Frontend Language' },
  { icon: 'F', name: 'Flutter', category: 'Mobile Framework' },
  { icon: 'D', name: 'Dart', category: 'Mobile Language' },
  { icon: 'M', name: 'MySQL', category: 'Database' },
  { icon: 'S', name: 'SQLite', category: 'Local Database' },
  { icon: 'B', name: 'Bootstrap', category: 'UI Framework' },
  { icon: 'T', name: 'Tailwind CSS', category: 'CSS Framework' },
  { icon: 'G', name: 'Git & GitHub', category: 'Version Control' },
  { icon: 'U', name: 'Ubuntu & Nginx', category: 'Deployment' },
]

const workflowSteps = [
  {
    icon: '◌',
    title: 'Understand',
    description:
      'Understand business goals, users, workflow, permissions, modules, and expected results.',
  },
  {
    icon: '✎',
    title: 'Plan',
    description:
      'Prepare application architecture, database structure, API flow, and development roadmap.',
  },
  {
    icon: '⌨',
    title: 'Build',
    description:
      'Develop backend logic, interfaces, integrations, mobile features, and required automation.',
  },
  {
    icon: '✓',
    title: 'Test',
    description:
      'Test workflows, permissions, responsiveness, API responses, edge cases, and stability.',
  },
  {
    icon: '↗',
    title: 'Deploy',
    description:
      'Prepare production builds, configure server services, SSL, queues, cron jobs, and domains.',
  },
]

const strengths = [
  {
    icon: '⚡',
    title: 'Problem Solving',
    description:
      'Breaking complex business requirements into practical and maintainable technical solutions.',
  },
  {
    icon: '✦',
    title: 'Clean Code',
    description:
      'Writing organized code that is easier to understand, test, maintain, and extend.',
  },
  {
    icon: '◉',
    title: 'Responsive Design',
    description:
      'Creating interfaces that work properly across desktop, tablet, and mobile devices.',
  },
  {
    icon: '⌘',
    title: 'Debugging',
    description:
      'Finding the actual cause of errors and applying reliable fixes instead of temporary patches.',
  },
  {
    icon: '◆',
    title: 'Business Understanding',
    description:
      'Turning real business operations into efficient application modules and digital workflows.',
  },
  {
    icon: '✓',
    title: 'Communication',
    description:
      'Providing clear updates and keeping requirements, progress, and project decisions transparent.',
  },
]
</script>

<style scoped>
:global(:root) {
  --bg-main: #0d1117;
  --bg-soft: #151a21;
  --card-bg: #161b22;
  --glass-bg: rgba(22, 27, 34, 0.88);
  --text-main: #e6edf3;
  --text-muted: #9aa4b2;
  --border: #2f3742;
  --gold: #f5a623;
  --gold-dark: #d78d13;
  --gold-soft: rgba(245, 166, 35, 0.12);
  --grid-color: rgba(255, 255, 255, 0.035);
  --shadow-color: rgba(0, 0, 0, 0.28);
}

:global(html[data-theme='light']) {
  --bg-main: #f8f7f2;
  --bg-soft: #ffffff;
  --card-bg: #ffffff;
  --glass-bg: rgba(255, 255, 255, 0.92);
  --text-main: #111827;
  --text-muted: #636b78;
  --border: #ddd9cf;
  --gold: #c68414;
  --gold-dark: #a86c0b;
  --gold-soft: rgba(198, 132, 20, 0.12);
  --grid-color: rgba(17, 24, 39, 0.055);
  --shadow-color: rgba(75, 55, 15, 0.12);
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

.skills-page {
  min-height: 100vh;
  overflow: hidden;
  background: var(--bg-main);
  color: var(--text-main);
  font-family: 'Inter', system-ui, sans-serif;
  line-height: 1.6;
}

.container {
  width: 100%;
  max-width: 1160px;
  margin: 0 auto;
  padding: 0 24px;
}

.section {
  padding: 100px 0;
}

.section-label {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 16px;
  color: var(--gold);
  font-family: monospace;
  font-size: 11px;
  font-weight: 800;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.section-label::before {
  width: 32px;
  height: 1px;
  background: var(--gold);
  content: '';
}

/* HERO */

.skills-hero {
  position: relative;
  display: flex;
  min-height: 100vh;
  align-items: center;
  padding: 145px 0 105px;
  overflow: hidden;
  isolation: isolate;
}

.trail-canvas {
  position: absolute;
  inset: 0;
  z-index: 4;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.hero-visual-bg {
  position: absolute;
  inset: 0;
  z-index: 0;
  overflow: hidden;
  background:
    radial-gradient(
      circle at var(--pointer-x) var(--pointer-y),
      var(--gold-soft),
      transparent 25%
    ),
    radial-gradient(
      circle at 13% 22%,
      rgba(245, 166, 35, 0.12),
      transparent 28%
    ),
    radial-gradient(
      circle at 87% 74%,
      rgba(245, 166, 35, 0.08),
      transparent 30%
    ),
    var(--bg-main);
}

.grid-layer {
  position: absolute;
  inset: -40px;
  background-image:
    linear-gradient(var(--grid-color) 1px, transparent 1px),
    linear-gradient(90deg, var(--grid-color) 1px, transparent 1px);
  background-size: 52px 52px;
  mask-image: radial-gradient(
    circle 320px at var(--pointer-x) var(--pointer-y),
    #000 10%,
    rgba(0, 0, 0, 0.5) 50%,
    transparent 100%
  );
}

.cursor-light {
  position: absolute;
  left: var(--pointer-x);
  top: var(--pointer-y);
  width: 430px;
  height: 430px;
  border: 1px solid rgba(245, 166, 35, 0.08);
  border-radius: 50%;
  background:
    radial-gradient(
      circle,
      rgba(245, 166, 35, 0.16),
      rgba(245, 166, 35, 0.05) 36%,
      transparent 70%
    );
  filter: blur(3px);
  transform: translate(-50%, -50%);
  transition:
    left 0.06s linear,
    top 0.06s linear;
}

.cursor-light::before,
.cursor-light::after {
  position: absolute;
  top: 50%;
  left: 50%;
  background: rgba(245, 166, 35, 0.25);
  content: '';
  transform: translate(-50%, -50%);
}

.cursor-light::before {
  width: 100%;
  height: 1px;
}

.cursor-light::after {
  width: 1px;
  height: 100%;
}

.ambient {
  position: absolute;
  border-radius: 50%;
  background: var(--gold);
  filter: blur(120px);
  opacity: 0.12;
}

.ambient-one {
  top: -100px;
  left: -80px;
  width: 360px;
  height: 360px;
}

.ambient-two {
  right: -120px;
  bottom: -120px;
  width: 430px;
  height: 430px;
}

.decorative-particle {
  position: absolute;
  width: 8px;
  height: 8px;
  border: 1px solid var(--gold);
  border-radius: 50%;
  box-shadow: 0 0 18px rgba(245, 166, 35, 0.55);
  animation: decorativeFloat 5s ease-in-out infinite;
}

@keyframes decorativeFloat {
  0%,
  100% {
    opacity: 0.35;
    transform: translateY(0) scale(0.8);
  }

  50% {
    opacity: 1;
    transform: translateY(-18px) scale(1.15);
  }
}

.hero-grid {
  position: relative;
  z-index: 5;
  display: grid;
  grid-template-columns: 0.95fr 1.05fr;
  align-items: center;
  gap: 58px;
}

.hero-copy {
  transition: transform 0.16s ease-out;
  will-change: transform;
}

.hero-copy h1 {
  max-width: 650px;
  margin: 0 0 24px;
  color: var(--text-main);
  font-size: clamp(33px, 4.2vw, 60px);
  font-weight: 900;
  line-height: 1.04;
  letter-spacing: -3px;
}

.hero-copy h1 span {
  display: block;
  color: var(--gold);
  text-shadow: 0 12px 40px rgba(245, 166, 35, 0.12);
}

.hero-description {
  max-width: 630px;
  margin: 0;
  color: var(--text-muted);
  font-size: 15px;
  line-height: 1.9;
}

.hero-actions,
.contact-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 13px;
  margin-top: 32px;
}

.btn-primary,
.btn-outline {
  display: inline-flex;
  min-height: 50px;
  align-items: center;
  justify-content: center;
  padding: 12px 29px;
  border: 1.5px solid var(--gold);
  border-radius: 10px;
  font-size: 13px;
  font-weight: 800;
  text-decoration: none;
  transition: 0.28s ease;
}

.btn-primary {
  background: var(--gold);
  color: #0d1117;
  box-shadow: 0 13px 30px rgba(245, 166, 35, 0.18);
}

.btn-primary:hover {
  transform: translateY(-3px);
  background: transparent;
  color: var(--gold);
}

.btn-outline {
  border-color: var(--border);
  background: var(--glass-bg);
  color: var(--text-main);
}

.btn-outline:hover {
  transform: translateY(-3px);
  border-color: var(--gold);
  background: var(--gold);
  color: #0d1117;
}

.hero-stats {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 44px;
}

.hero-stats article {
  min-width: 142px;
  padding: 15px 17px;
  border: 1px solid var(--border);
  border-radius: 14px;
  background: var(--glass-bg);
  box-shadow: 0 14px 35px var(--shadow-color);
  backdrop-filter: blur(14px);
  transition: 0.25s ease;
}

.hero-stats article:hover {
  transform: translateY(-5px);
  border-color: rgba(245, 166, 35, 0.55);
}

.hero-stats strong,
.hero-stats span {
  display: block;
}

.hero-stats strong {
  color: var(--gold);
  font-size: 23px;
  line-height: 1;
}

.hero-stats span {
  margin-top: 7px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 8px;
  letter-spacing: 0.7px;
  text-transform: uppercase;
}

/* CONSTELLATION */

.visual-column {
  display: flex;
  justify-content: center;
}

.skill-constellation {
  position: relative;
  width: 580px;
  height: 580px;
  transform-style: preserve-3d;
  transition: transform 0.14s ease-out;
  will-change: transform;
}

.constellation-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 390px;
  height: 390px;
  border-radius: 50%;
  background:
    radial-gradient(circle, var(--gold-soft), transparent 68%);
  filter: blur(10px);
  transform: translate(-50%, -50%);
  animation: corePulse 3.5s ease-in-out infinite;
}

@keyframes corePulse {
  0%,
  100% {
    opacity: 0.55;
    transform: translate(-50%, -50%) scale(0.94);
  }

  50% {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1.06);
  }
}

.constellation-lines {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  overflow: visible;
}

.constellation-lines line,
.constellation-lines circle {
  fill: none;
  stroke: rgba(245, 166, 35, 0.24);
  stroke-width: 1;
}

.constellation-lines circle:last-child {
  stroke-dasharray: 5 8;
  animation: dashRotate 18s linear infinite;
  transform-origin: center;
}

@keyframes dashRotate {
  to {
    transform: rotate(360deg);
  }
}

.constellation-core {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 6;
  display: flex;
  width: 160px;
  height: 160px;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  border: 1px solid rgba(245, 166, 35, 0.52);
  border-radius: 50%;
  background:
    radial-gradient(
      circle at 35% 28%,
      rgba(245, 166, 35, 0.22),
      transparent 38%
    ),
    var(--card-bg);
  box-shadow:
    0 0 55px rgba(245, 166, 35, 0.18),
    0 30px 65px var(--shadow-color),
    inset 0 0 35px rgba(245, 166, 35, 0.08);
  transform: translate(-50%, -50%) translateZ(45px);
}

.constellation-core::before {
  position: absolute;
  inset: 10px;
  border: 1px dashed rgba(245, 166, 35, 0.3);
  border-radius: 50%;
  content: '';
  animation: coreSpin 13s linear infinite;
}

@keyframes coreSpin {
  to {
    transform: rotate(360deg);
  }
}

.constellation-core span,
.constellation-core small {
  position: relative;
  font-family: monospace;
  letter-spacing: 1.6px;
  text-transform: uppercase;
}

.constellation-core span {
  color: var(--text-muted);
  font-size: 8px;
}

.constellation-core strong {
  position: relative;
  margin: 5px 0;
  color: var(--gold);
  font-size: 44px;
  line-height: 1;
}

.constellation-core small {
  color: var(--text-main);
  font-size: 8px;
}

.skill-node {
  position: absolute;
  z-index: 8;
  display: flex;
  min-width: 128px;
  align-items: center;
  gap: 10px;
  padding: 11px 13px;
  border: 1px solid var(--border);
  border-radius: 14px;
  background: var(--glass-bg);
  color: var(--text-main);
  box-shadow: 0 18px 42px var(--shadow-color);
  text-align: left;
  backdrop-filter: blur(16px);
  transition:
    transform 0.13s ease-out,
    border-color 0.25s ease,
    box-shadow 0.25s ease;
  cursor: pointer;
}

.skill-node:hover {
  border-color: rgba(245, 166, 35, 0.65);
  box-shadow:
    0 22px 48px var(--shadow-color),
    0 0 25px rgba(245, 166, 35, 0.13);
}

.skill-node > span {
  display: flex;
  width: 34px;
  height: 34px;
  flex: 0 0 34px;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(245, 166, 35, 0.18);
  border-radius: 10px;
  background: var(--gold-soft);
  color: var(--gold);
  font-family: monospace;
  font-size: 13px;
  font-weight: 900;
}

.skill-node strong,
.skill-node small {
  display: block;
}

.skill-node strong {
  color: var(--text-main);
  font-size: 11px;
}

.skill-node small {
  margin-top: 2px;
  color: var(--text-muted);
  font-size: 8px;
}

.node-laravel {
  top: 18px;
  left: 226px;
}

.node-vue {
  top: 122px;
  right: -4px;
}

.node-flutter {
  right: -2px;
  bottom: 112px;
}

.node-mysql {
  bottom: 15px;
  left: 226px;
}

.node-php {
  bottom: 112px;
  left: -2px;
}

.node-git {
  top: 122px;
  left: -5px;
}

.floating-terminal {
  position: absolute;
  right: 63px;
  bottom: 35px;
  z-index: 9;
  width: 185px;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 14px;
  background: #10141a;
  box-shadow: 0 22px 50px rgba(0, 0, 0, 0.27);
  transform: translateZ(60px);
  animation: terminalFloat 4s ease-in-out infinite;
}

@keyframes terminalFloat {
  0%,
  100% {
    margin-bottom: 0;
  }

  50% {
    margin-bottom: 10px;
  }
}

.terminal-head {
  display: flex;
  min-height: 32px;
  align-items: center;
  gap: 5px;
  padding: 0 9px;
  border-bottom: 1px solid #29303a;
}

.terminal-head span {
  width: 6px;
  height: 6px;
  border-radius: 50%;
}

.terminal-head span:nth-child(1) {
  background: #ff5f57;
}

.terminal-head span:nth-child(2) {
  background: #febc2e;
}

.terminal-head span:nth-child(3) {
  background: #28c840;
}

.terminal-head small {
  margin-left: auto;
  color: #7f8b99;
  font-family: monospace;
  font-size: 7px;
}

.terminal-code {
  padding: 12px 14px;
  color: #d8dee9;
  font-family: monospace;
  font-size: 8px;
  line-height: 1.65;
}

.terminal-code p {
  margin: 0;
}

.terminal-code em {
  color: #c792ea;
  font-style: normal;
}

.scroll-hint {
  position: absolute;
  bottom: 23px;
  left: 50%;
  z-index: 6;
  display: flex;
  align-items: center;
  gap: 10px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 8px;
  letter-spacing: 1.6px;
  text-transform: uppercase;
  transform: translateX(-50%);
}

.scroll-hint i {
  position: relative;
  display: block;
  width: 40px;
  height: 1px;
  overflow: hidden;
  background: var(--border);
}

.scroll-hint i::after {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 1px;
  background: var(--gold);
  content: '';
  animation: scrollLine 2s linear infinite;
}

@keyframes scrollLine {
  to {
    left: 100%;
  }
}

/* TICKER */

.skills-ticker {
  overflow: hidden;
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background: var(--bg-soft);
}

.ticker-track {
  display: flex;
  width: max-content;
  gap: 46px;
  padding: 15px 0;
  white-space: nowrap;
  animation: tickerMove 26s linear infinite;
}

.ticker-track span {
  color: var(--text-muted);
  font-family: monospace;
  font-size: 11px;
}

.ticker-track b {
  margin-right: 9px;
  color: var(--gold);
}

@keyframes tickerMove {
  to {
    transform: translateX(-50%);
  }
}

/* HEADINGS */

.section-heading {
  display: grid;
  grid-template-columns: 1fr 0.8fr;
  align-items: end;
  gap: 75px;
  margin-bottom: 58px;
}

.section-heading h2,
.center-heading h2,
.proficiency-copy h2 {
  max-width: 690px;
  margin: 0;
  font-size: clamp(31px, 4vw, 48px);
  font-weight: 900;
  line-height: 1.12;
  letter-spacing: -1.7px;
}

.section-heading > p,
.center-heading > p,
.proficiency-copy > p {
  margin: 0;
  color: var(--text-muted);
  font-size: 14px;
  line-height: 1.85;
}

.center-heading {
  max-width: 790px;
  margin: 0 auto 60px;
  text-align: center;
}

.center-heading .section-label {
  justify-content: center;
}

.center-heading .section-label::after {
  width: 32px;
  height: 1px;
  background: var(--gold);
  content: '';
}

.center-heading h2 {
  margin: 0 auto 17px;
}

.center-heading p {
  max-width: 660px;
  margin: auto;
}

/* EXPERTISE */

.expertise-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.expertise-card {
  position: relative;
  min-height: 330px;
  padding: 26px;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 19px;
  background:
    linear-gradient(
      145deg,
      var(--glass-bg),
      color-mix(in srgb, var(--card-bg) 88%, transparent)
    );
  box-shadow: 0 18px 45px var(--shadow-color);
  transition: 0.28s ease;
}

.expertise-card::after {
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  height: 2px;
  background:
    linear-gradient(90deg, transparent, var(--gold), transparent);
  content: '';
  opacity: 0;
  transform: scaleX(0.25);
  transition: 0.3s ease;
}

.expertise-card:hover {
  transform: translateY(-6px);
  border-color: rgba(245, 166, 35, 0.5);
}

.expertise-card:hover::after {
  opacity: 1;
  transform: scaleX(1);
}

.expertise-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 24px;
}

.expertise-icon {
  display: flex;
  width: 48px;
  height: 48px;
  align-items: center;
  justify-content: center;
  border-radius: 14px;
  background: var(--gold-soft);
  color: var(--gold);
  font-size: 20px;
}

.expertise-number {
  color: color-mix(in srgb, var(--gold) 20%, transparent);
  font-size: 36px;
  font-weight: 900;
  line-height: 1;
}

.expertise-card h3 {
  margin: 0 0 9px;
  font-size: 18px;
}

.expertise-card > p {
  min-height: 74px;
  margin: 0 0 19px;
  color: var(--text-muted);
  font-size: 12px;
  line-height: 1.8;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
}

.skill-tags span {
  padding: 5px 9px;
  border: 1px solid rgba(245, 166, 35, 0.2);
  border-radius: 100px;
  background: var(--gold-soft);
  color: var(--gold);
  font-family: monospace;
  font-size: 9px;
}

/* PROFICIENCY */

.proficiency-section {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background: var(--bg-soft);
}

.proficiency-grid {
  display: grid;
  grid-template-columns: 0.85fr 1.15fr;
  align-items: center;
  gap: 80px;
}

.proficiency-copy h2 {
  margin-bottom: 19px;
}

.experience-note {
  display: flex;
  align-items: flex-start;
  gap: 13px;
  margin-top: 30px;
  padding: 19px;
  border: 1px solid var(--border);
  border-radius: 15px;
  background: var(--glass-bg);
}

.experience-note > span {
  display: flex;
  width: 38px;
  height: 38px;
  flex: 0 0 38px;
  align-items: center;
  justify-content: center;
  border-radius: 11px;
  background: var(--gold-soft);
  color: var(--gold);
}

.experience-note p {
  margin: 0;
  color: var(--text-muted);
  font-size: 12px;
  line-height: 1.8;
}

.progress-panel {
  padding: 29px;
  border: 1px solid var(--border);
  border-radius: 22px;
  background: var(--card-bg);
  box-shadow: 0 22px 55px var(--shadow-color);
}

.progress-item {
  margin-bottom: 27px;
}

.progress-item:last-child {
  margin-bottom: 0;
}

.progress-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}

.progress-header > div {
  display: flex;
  align-items: center;
  gap: 10px;
}

.progress-header > div > span {
  display: flex;
  width: 29px;
  height: 29px;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  background: var(--gold-soft);
  color: var(--gold);
  font-family: monospace;
  font-size: 10px;
  font-weight: 900;
}

.progress-header strong {
  font-size: 12px;
}

.progress-header > b {
  color: var(--gold);
  font-family: monospace;
  font-size: 10px;
}

.progress-track {
  height: 8px;
  overflow: hidden;
  border-radius: 100px;
  background: color-mix(in srgb, var(--text-main) 8%, transparent);
}

.progress-track span {
  position: relative;
  display: block;
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(90deg, var(--gold-dark), var(--gold));
  animation: progressReveal 1.5s ease both;
}

.progress-track span::after {
  position: absolute;
  top: 50%;
  right: 0;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: var(--gold);
  box-shadow: 0 0 16px rgba(245, 166, 35, 0.8);
  content: '';
  transform: translate(20%, -50%);
}

@keyframes progressReveal {
  from {
    width: 0;
  }
}

.progress-item > p {
  margin: 7px 0 0;
  color: var(--text-muted);
  font-size: 9px;
  line-height: 1.6;
}

/* TOOLS */

.tool-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 15px;
}

.tool-card {
  position: relative;
  display: flex;
  min-height: 108px;
  align-items: center;
  gap: 13px;
  padding: 18px;
  border: 1px solid var(--border);
  border-radius: 15px;
  background: var(--glass-bg);
  box-shadow: 0 14px 35px var(--shadow-color);
  transition: 0.26s ease;
}

.tool-card:hover {
  transform: translateY(-5px);
  border-color: rgba(245, 166, 35, 0.5);
  background: var(--gold-soft);
}

.tool-icon {
  display: flex;
  width: 43px;
  height: 43px;
  flex: 0 0 43px;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  background: var(--gold-soft);
  color: var(--gold);
  font-family: monospace;
  font-weight: 900;
}

.tool-card h3 {
  margin: 0;
  font-size: 12px;
}

.tool-card p {
  margin: 3px 0 0;
  color: var(--text-muted);
  font-size: 9px;
}

.tool-card small {
  position: absolute;
  top: 9px;
  right: 10px;
  display: flex;
  align-items: center;
  gap: 5px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 7px;
  text-transform: uppercase;
}

.tool-card small i {
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: var(--gold);
  box-shadow: 0 0 8px rgba(245, 166, 35, 0.7);
}

/* WORKFLOW */

.workflow-section {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background:
    radial-gradient(
      circle at 12% 90%,
      rgba(245, 166, 35, 0.06),
      transparent 30%
    ),
    var(--bg-soft);
}

.workflow-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 16px;
}

.workflow-card {
  position: relative;
  min-height: 265px;
  padding: 24px;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 18px;
  background: var(--card-bg);
  box-shadow: 0 18px 45px var(--shadow-color);
  transition: 0.28s ease;
}

.workflow-card:hover {
  transform: translateY(-6px);
  border-color: rgba(245, 166, 35, 0.5);
}

.workflow-number {
  position: absolute;
  top: 8px;
  right: 14px;
  color: color-mix(in srgb, var(--gold) 12%, transparent);
  font-size: 54px;
  font-weight: 900;
  line-height: 1;
}

.workflow-icon {
  display: flex;
  width: 44px;
  height: 44px;
  align-items: center;
  justify-content: center;
  margin-bottom: 42px;
  border-radius: 13px;
  background: var(--gold-soft);
  color: var(--gold);
}

.workflow-card h3 {
  margin: 0 0 9px;
  font-size: 15px;
}

.workflow-card p {
  margin: 0;
  color: var(--text-muted);
  font-size: 11px;
  line-height: 1.75;
}

/* STRENGTHS */

.strength-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

.strength-card {
  padding: 24px;
  border: 1px solid var(--border);
  border-radius: 17px;
  background: var(--glass-bg);
  box-shadow: 0 16px 40px var(--shadow-color);
  transition: 0.27s ease;
}

.strength-card:hover {
  transform: translateY(-5px);
  border-color: rgba(245, 166, 35, 0.48);
}

.strength-card > span {
  display: flex;
  width: 44px;
  height: 44px;
  align-items: center;
  justify-content: center;
  margin-bottom: 18px;
  border-radius: 13px;
  background: var(--gold-soft);
  color: var(--gold);
}

.strength-card h3 {
  margin: 0 0 7px;
  font-size: 15px;
}

.strength-card p {
  margin: 0;
  color: var(--text-muted);
  font-size: 11px;
  line-height: 1.8;
}

/* CONTACT */

.contact-section {
  padding-top: 35px;
}

.contact-box {
  position: relative;
  padding: 74px 40px;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 28px;
  background:
    linear-gradient(
      145deg,
      rgba(245, 166, 35, 0.09),
      var(--glass-bg)
    );
  box-shadow: 0 25px 65px var(--shadow-color);
  text-align: center;
}

.contact-glow {
  position: absolute;
  top: -150px;
  left: 50%;
  width: 400px;
  height: 300px;
  border-radius: 50%;
  background: var(--gold);
  filter: blur(125px);
  opacity: 0.11;
  transform: translateX(-50%);
}

.availability {
  position: relative;
  display: inline-flex;
  align-items: center;
  gap: 9px;
  margin-bottom: 21px;
  color: var(--gold);
  font-family: monospace;
  font-size: 10px;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.availability span {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--gold);
  animation: availabilityPulse 1.8s infinite;
}

@keyframes availabilityPulse {
  0%,
  100% {
    box-shadow: 0 0 0 5px var(--gold-soft);
  }

  50% {
    box-shadow: 0 0 0 10px transparent;
  }
}

.contact-box h2 {
  position: relative;
  max-width: 760px;
  margin: 0 auto 15px;
  font-size: clamp(34px, 5vw, 54px);
  font-weight: 900;
  line-height: 1.12;
  letter-spacing: -1.8px;
}

.contact-box > p {
  position: relative;
  max-width: 680px;
  margin: auto;
  color: var(--text-muted);
  font-size: 14px;
  line-height: 1.85;
}

.contact-actions {
  position: relative;
  justify-content: center;
}

/* FOOTER */

.footer {
  padding: 28px 0;
  border-top: 1px solid var(--border);
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  gap: 12px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 10px;
}

/* RESPONSIVE */

@media (max-width: 1080px) {
  .hero-grid {
    gap: 30px;
  }

  .skill-constellation {
    width: 500px;
    height: 500px;
  }

  .node-laravel {
    left: 185px;
  }

  .node-mysql {
    left: 185px;
  }

  .expertise-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .tool-grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .workflow-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 880px) {
  .skills-hero {
    padding-top: 130px;
  }

  .hero-grid,
  .section-heading,
  .proficiency-grid {
    grid-template-columns: 1fr;
  }

  .hero-grid {
    gap: 55px;
  }

  .hero-copy {
    text-align: center;
  }

  .section-label {
    justify-content: center;
  }

  .section-label::after {
    width: 32px;
    height: 1px;
    background: var(--gold);
    content: '';
  }

  .hero-copy h1,
  .hero-description {
    margin-right: auto;
    margin-left: auto;
  }

  .hero-actions,
  .hero-stats {
    justify-content: center;
  }

  .section-heading {
    gap: 20px;
  }

  .proficiency-copy {
    text-align: center;
  }

  .proficiency-copy > p {
    max-width: 650px;
    margin: auto;
  }

  .experience-note {
    max-width: 620px;
    margin-right: auto;
    margin-left: auto;
    text-align: left;
  }

  .strength-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 650px) {
  .container {
    padding: 0 18px;
  }

  .section {
    padding: 74px 0;
  }

  .skills-hero {
    min-height: auto;
    padding: 115px 0 72px;
  }

  .hero-copy h1 {
    font-size: 38px;
    letter-spacing: -1.6px;
  }

  .hero-description {
    font-size: 14px;
  }

  .hero-actions,
  .contact-actions {
    flex-direction: column;
  }

  .btn-primary,
  .btn-outline {
    width: 100%;
  }

  .hero-stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 8px;
  }

  .hero-stats article {
    min-width: 0;
    padding: 13px 7px;
  }

  .hero-stats strong {
    font-size: 20px;
  }

  .hero-stats span {
    font-size: 7px;
  }

  .skill-constellation {
    width: 340px;
    height: 410px;
  }

  .constellation-lines {
    top: 32px;
    transform: scale(0.66);
  }

  .constellation-core {
    top: 45%;
    width: 125px;
    height: 125px;
  }

  .constellation-core strong {
    font-size: 34px;
  }

  .skill-node {
    min-width: 94px;
    padding: 7px 8px;
  }

  .skill-node > span {
    width: 26px;
    height: 26px;
    flex-basis: 26px;
    font-size: 10px;
  }

  .skill-node strong {
    font-size: 8px;
  }

  .skill-node small {
    font-size: 6px;
  }

  .node-laravel {
    top: 0;
    left: 122px;
  }

  .node-vue {
    top: 82px;
    right: -1px;
  }

  .node-flutter {
    right: -1px;
    bottom: 67px;
  }

  .node-mysql {
    bottom: 0;
    left: 122px;
  }

  .node-php {
    bottom: 67px;
    left: -1px;
  }

  .node-git {
    top: 82px;
    left: -1px;
  }

  .floating-terminal {
    right: 66px;
    bottom: 48px;
    width: 155px;
  }

  .terminal-code {
    font-size: 7px;
  }

  .scroll-hint {
    display: none;
  }

  .expertise-grid,
  .tool-grid,
  .workflow-grid,
  .strength-grid {
    grid-template-columns: 1fr;
  }

  .expertise-card {
    min-height: 0;
  }

  .expertise-card > p {
    min-height: 0;
  }

  .section-heading h2,
  .center-heading h2,
  .proficiency-copy h2 {
    font-size: 33px;
  }

  .progress-panel {
    padding: 22px 18px;
  }

  .workflow-card {
    min-height: 230px;
  }

  .contact-box {
    padding: 52px 22px;
  }

  .contact-box h2 {
    font-size: 34px;
  }

  .footer-inner {
    flex-direction: column;
    text-align: center;
  }
}

@media (max-width: 380px) {
  .hero-copy h1 {
    font-size: 33px;
  }

  .skill-constellation {
    width: 300px;
  }

  .node-laravel,
  .node-mysql {
    left: 102px;
  }

  .floating-terminal {
    right: 48px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .skill-constellation,
  .hero-copy,
  .decorative-particle,
  .constellation-glow,
  .constellation-lines circle,
  .constellation-core::before,
  .floating-terminal,
  .ticker-track,
  .scroll-hint i::after {
    animation: none;
    transform: none !important;
  }
}
</style>

<template>
  <div class="about-page">
    <nav-component />

    <!-- =========================
         ABOUT HERO BANNER
    ========================== -->
    <section
      ref="heroSection"
      class="about-hero"
      @mousemove="handleMouseMove"
      @mouseleave="resetMouseEffects"
    >
      <!-- Mouse particles -->
      <canvas ref="trailCanvas" class="trail-canvas"></canvas>

      <!-- Background -->
      <div class="hero-background">
        <span
          class="mouse-glow"
          :style="mouseGlowStyle"
        ></span>

        <span
          class="glow glow-one"
          :style="{
            transform: `translate3d(${mouseX * 22}px, ${mouseY * 22}px, 0)`
          }"
        ></span>

        <span
          class="glow glow-two"
          :style="{
            transform: `translate3d(${mouseX * -28}px, ${mouseY * -28}px, 0)`
          }"
        ></span>

        <span
          class="floating-skill skill-one"
          :style="{
            transform: `translate3d(${mouseX * -18}px, ${mouseY * -18}px, 0)`
          }"
        >
          Laravel
        </span>

        <span
          class="floating-skill skill-two"
          :style="{
            transform: `translate3d(${mouseX * 22}px, ${mouseY * 22}px, 0)`
          }"
        >
          Vue.js
        </span>

        <span
          class="floating-skill skill-three"
          :style="{
            transform: `translate3d(${mouseX * -25}px, ${mouseY * 15}px, 0)`
          }"
        >
          Flutter
        </span>

        <span
          class="floating-skill skill-four"
          :style="{
            transform: `translate3d(${mouseX * 16}px, ${mouseY * -20}px, 0)`
          }"
        >
          MySQL
        </span>

        <span
          class="floating-skill skill-five"
          :style="{
            transform: `translate3d(${mouseX * -14}px, ${mouseY * 25}px, 0)`
          }"
        >
          REST API
        </span>
      </div>

      <div class="container">
        <div class="about-grid">
          <!-- =========================
               CIRCULAR PROFILE IMAGE
          ========================== -->
          <div class="image-column">
            <div
              class="profile-area"
              :style="profileTiltStyle"
            >
              <div class="profile-orbit orbit-one">
                <span></span>
              </div>

              <div class="profile-orbit orbit-two">
                <span></span>
              </div>

              <div class="profile-circle-border">
                <div class="profile-circle">
                  <img
                    src="/assets/images/bilal.png"
                    alt="Muhammad Bilal - Full Stack Developer"
                    class="profile-image"
                  />
                </div>
              </div>

              <div class="profile-code code-laravel">
                <span>◆</span>
                Laravel
              </div>

              <div class="profile-code code-vue">
                <span>◆</span>
                Vue.js
              </div>

              <div class="profile-code code-flutter">
                <span>◆</span>
                Flutter
              </div>

              <div class="experience-badge">
                <strong>2+</strong>

                <div>
                  <span>Years of</span>
                  <span>Experience</span>
                </div>
              </div>

              <div class="availability-card">
                <span class="availability-dot"></span>

                <div>
                  <strong>Available for projects</strong>
                  <small>Remote and freelance work</small>
                </div>
              </div>
            </div>
          </div>

          <!-- =========================
               ABOUT CONTENT
          ========================== -->
          <div class="content-column">
            <div class="section-label">About Me</div>

            <h1>
              Building digital products that
              <span>solve real problems.</span>
            </h1>

            <p class="intro-text">
              Hello, I’m
              <strong>Muhammad Bilal</strong>, a Full-Stack Web and Mobile App
              Developer based in Lahore, Pakistan.
            </p>

            <p class="description">
              I specialize in building modern, secure, and scalable applications
              using Laravel, Vue.js, Flutter, PHP, and MySQL. My focus is not
              only on writing code, but also on creating reliable digital
              solutions that help businesses improve their daily operations and
              grow efficiently.
            </p>

            <p class="description">
              From business management systems and CRM platforms to custom
              sportswear applications, REST APIs, dashboards, and mobile apps, I
              enjoy transforming complex requirements into clean and
              user-friendly products.
            </p>

            <div class="quick-details">
              <div class="detail-item">
                <span class="detail-icon">⌖</span>

                <div>
                  <small>Location</small>
                  <strong>Lahore, Pakistan</strong>
                </div>
              </div>

              <div class="detail-item">
                <span class="detail-icon">✦</span>

                <div>
                  <small>Specialization</small>
                  <strong>Web & Mobile Development</strong>
                </div>
              </div>

              <div class="detail-item">
                <span class="detail-icon">◉</span>

                <div>
                  <small>Core Stack</small>
                  <strong>Laravel, Vue.js & Flutter</strong>
                </div>
              </div>

              <div class="detail-item">
                <span class="detail-icon">✓</span>

                <div>
                  <small>Work Type</small>
                  <strong>Remote & Freelance</strong>
                </div>
              </div>
            </div>

            <div class="hero-actions">
              <a href="#about-contact" class="primary-button">
                Work With Me
              </a>

              <a
                href="/Muhammad-Bilal-Resume.pdf"
                download="Muhammad-Bilal-Resume.pdf"
                class="outline-button"
              >
                Download Resume
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="scroll-indicator">
        <span>Scroll</span>
        <div class="scroll-line"></div>
      </div>
    </section>

    <!-- =========================
         STATISTICS
    ========================== -->
    <section class="numbers-section">
      <div class="container">
        <div class="numbers-grid">
          <div
            v-for="item in statistics"
            :key="item.label"
            class="number-card"
          >
            <div class="number-value">{{ item.value }}</div>
            <div class="number-label">{{ item.label }}</div>
          </div>
        </div>
      </div>
    </section>

    <!-- =========================
         MY STORY
    ========================== -->
    <section class="section story-section">
      <div class="container">
        <div class="section-heading">
          <div>
            <div class="section-label">My Story</div>

            <h2>
              From learning code to building real products.
            </h2>
          </div>

          <p>
            My development journey has been driven by curiosity, continuous
            learning, and a strong interest in building useful products.
          </p>
        </div>

        <div class="story-grid">
          <div class="story-content">
            <div
              v-for="story in stories"
              :key="story.number"
              class="story-block"
            >
              <span class="story-number">{{ story.number }}</span>

              <div>
                <h3>{{ story.title }}</h3>
                <p>{{ story.description }}</p>
              </div>
            </div>
          </div>

          <div class="code-card">
            <div class="code-card-header">
              <div class="window-buttons">
                <span></span>
                <span></span>
                <span></span>
              </div>

              <span>developer-profile.js</span>
            </div>

            <div class="code-content">
              <p>
                <span class="code-purple">const</span>
                <span class="code-white"> developer </span>
                <span class="code-purple">=</span>
                <span class="code-white"> {</span>
              </p>

              <p class="code-indent">
                <span class="code-blue">name:</span>
                <span class="code-green">'Muhammad Bilal'</span>,
              </p>

              <p class="code-indent">
                <span class="code-blue">role:</span>
                <span class="code-green">'Full Stack Developer'</span>,
              </p>

              <p class="code-indent">
                <span class="code-blue">backend:</span>
                <span class="code-green">'Laravel & PHP'</span>,
              </p>

              <p class="code-indent">
                <span class="code-blue">frontend:</span>
                <span class="code-green">'Vue.js'</span>,
              </p>

              <p class="code-indent">
                <span class="code-blue">mobile:</span>
                <span class="code-green">'Flutter'</span>,
              </p>

              <p class="code-indent">
                <span class="code-blue">database:</span>
                <span class="code-green">'MySQL'</span>,
              </p>

              <p class="code-indent">
                <span class="code-blue">passion:</span>
                <span class="code-green">'Building useful products'</span>,
              </p>

              <p>
                <span class="code-white">}</span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- =========================
         CAREER JOURNEY
    ========================== -->
    <section class="section journey-section">
      <div class="container">
        <div class="center-heading">
          <div class="section-label">Career Journey</div>

          <h2>
            Experience that shaped my development skills.
          </h2>

          <p>
            Every role has helped me improve my technical knowledge,
            communication, and understanding of real business requirements.
          </p>
        </div>

        <div class="timeline">
          <div
            v-for="experience in experiences"
            :key="experience.company"
            class="timeline-item"
          >
            <div class="timeline-date">
              {{ experience.date }}
            </div>

            <div class="timeline-marker">
              <span></span>
            </div>

            <div class="timeline-card">
              <div class="timeline-top">
                <div>
                  <h3>{{ experience.role }}</h3>
                  <h4>{{ experience.company }}</h4>
                </div>

                <span class="location-badge">
                  {{ experience.location }}
                </span>
              </div>

              <p>{{ experience.description }}</p>

              <div class="timeline-tags">
                <span
                  v-for="technology in experience.technologies"
                  :key="technology"
                >
                  {{ technology }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- =========================
         TECHNICAL EXPERTISE
    ========================== -->
    <section class="section expertise-section">
      <div class="container">
        <div class="section-heading">
          <div>
            <div class="section-label">Technical Expertise</div>

            <h2>
              Technologies I use to build products.
            </h2>
          </div>

          <p>
            I choose technologies based on project requirements, scalability,
            performance, security, and long-term maintainability.
          </p>
        </div>

        <div class="expertise-grid">
          <div
            v-for="group in skillGroups"
            :key="group.title"
            class="expertise-card"
          >
            <div class="expertise-icon">
              {{ group.icon }}
            </div>

            <h3>{{ group.title }}</h3>

            <p>{{ group.description }}</p>

            <div class="skill-list">
              <span
                v-for="skill in group.skills"
                :key="skill"
              >
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- =========================
         DEVELOPMENT PROCESS
    ========================== -->
    <section class="section process-section">
      <div class="container">
        <div class="center-heading">
          <div class="section-label">My Process</div>

          <h2>
            How I turn an idea into a working product.
          </h2>
        </div>

        <div class="process-grid">
          <div
            v-for="(step, index) in processSteps"
            :key="step.title"
            class="process-card"
          >
            <div class="process-number">
              {{ String(index + 1).padStart(2, '0') }}
            </div>

            <div class="process-icon">
              {{ step.icon }}
            </div>

            <h3>{{ step.title }}</h3>
            <p>{{ step.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- =========================
         VALUES
    ========================== -->
    <section class="section values-section">
      <div class="container">
        <div class="section-heading">
          <div>
            <div class="section-label">Development Values</div>

            <h2>
              What you can expect when working with me.
            </h2>
          </div>

          <p>
            A successful product requires more than code. It requires clear
            communication, responsibility, proper planning, and attention to
            every detail.
          </p>
        </div>

        <div class="values-grid">
          <div
            v-for="value in values"
            :key="value.title"
            class="value-card"
          >
            <span class="value-icon">
              {{ value.icon }}
            </span>

            <div>
              <h3>{{ value.title }}</h3>
              <p>{{ value.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- =========================
         CONTACT CTA
    ========================== -->
    <section class="section contact-section" id="about-contact">
      <div class="container">
        <div class="contact-box">
          <div class="contact-glow"></div>

          <div class="available-text">
            <span></span>
            Available for new opportunities
          </div>

          <h2>
            Let’s build something valuable together.
          </h2>

          <p>
            Have a website, business system, dashboard, API, or mobile app in
            mind? Share your idea and let’s turn it into a reliable product.
          </p>

          <div class="contact-actions">
            <a
              href="mailto:itbilal73@gmail.com"
              class="primary-button"
            >
              Start a Project
            </a>

            <a
              href="tel:03015825174"
              class="outline-button"
            >
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
  ref,
  computed,
  onMounted,
  onBeforeUnmount,
} from 'vue'

const heroSection = ref(null)
const trailCanvas = ref(null)

const mouseX = ref(0)
const mouseY = ref(0)
const mousePixelX = ref(0)
const mousePixelY = ref(0)

let canvasContext = null
let particles = []
let animationFrame = null

const mouseGlowStyle = computed(() => ({
  left: `${mousePixelX.value}px`,
  top: `${mousePixelY.value}px`,
}))

const profileTiltStyle = computed(() => ({
  transform: `
    perspective(1100px)
    rotateX(${mouseY.value * -4}deg)
    rotateY(${mouseX.value * 5}deg)
    translate3d(${mouseX.value * 8}px, ${mouseY.value * 8}px, 0)
  `,
}))

const resizeCanvas = () => {
  const canvas = trailCanvas.value

  if (!canvas) {
    return
  }

  const rect = canvas.getBoundingClientRect()
  const devicePixelRatio = window.devicePixelRatio || 1

  canvas.width = rect.width * devicePixelRatio
  canvas.height = rect.height * devicePixelRatio

  canvas.style.width = `${rect.width}px`
  canvas.style.height = `${rect.height}px`

  canvasContext = canvas.getContext('2d')

  if (canvasContext) {
    canvasContext.setTransform(
      devicePixelRatio,
      0,
      0,
      devicePixelRatio,
      0,
      0,
    )
  }
}

const createMouseParticles = (x, y) => {
  for (let index = 0; index < 3; index += 1) {
    particles.push({
      x,
      y,
      size: Math.random() * 2.4 + 0.8,
      speedX: (Math.random() - 0.5) * 1.8,
      speedY: (Math.random() - 0.5) * 1.8,
      opacity: Math.random() * 0.45 + 0.45,
      life: 1,
    })
  }

  if (particles.length > 120) {
    particles = particles.slice(-120)
  }
}

const handleMouseMove = (event) => {
  const section = heroSection.value

  if (!section) {
    return
  }

  const rect = section.getBoundingClientRect()

  const relativeX = event.clientX - rect.left
  const relativeY = event.clientY - rect.top

  mousePixelX.value = relativeX
  mousePixelY.value = relativeY

  mouseX.value = relativeX / rect.width - 0.5
  mouseY.value = relativeY / rect.height - 0.5

  createMouseParticles(relativeX, relativeY)
}

const resetMouseEffects = () => {
  mouseX.value = 0
  mouseY.value = 0
}

const animateParticles = () => {
  const canvas = trailCanvas.value

  if (!canvas || !canvasContext) {
    animationFrame = requestAnimationFrame(animateParticles)
    return
  }

  const rect = canvas.getBoundingClientRect()

  canvasContext.clearRect(
    0,
    0,
    rect.width,
    rect.height,
  )

  particles.forEach((particle) => {
    particle.x += particle.speedX
    particle.y += particle.speedY
    particle.life -= 0.022
    particle.size *= 0.992

    const currentOpacity = Math.max(
      particle.opacity * particle.life,
      0,
    )

    canvasContext.beginPath()

    canvasContext.arc(
      particle.x,
      particle.y,
      Math.max(particle.size, 0.2),
      0,
      Math.PI * 2,
    )

    canvasContext.fillStyle = `rgba(
      245,
      166,
      35,
      ${currentOpacity}
    )`

    canvasContext.shadowBlur = 15
    canvasContext.shadowColor = 'rgba(245, 166, 35, 0.75)'
    canvasContext.fill()
  })

  particles = particles.filter(
    (particle) => particle.life > 0,
  )

  animationFrame = requestAnimationFrame(animateParticles)
}

onMounted(() => {
  resizeCanvas()

  window.addEventListener('resize', resizeCanvas)

  animationFrame = requestAnimationFrame(
    animateParticles,
  )
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeCanvas)

  if (animationFrame) {
    cancelAnimationFrame(animationFrame)
  }

  particles = []
})

const statistics = [
  {
    value: '2+',
    label: 'Years Experience',
  },
  {
    value: '10+',
    label: 'Completed Projects',
  },
  {
    value: '6+',
    label: 'Core Technologies',
  },
  {
    value: '100%',
    label: 'Commitment',
  },
]

const stories = [
  {
    number: '01',
    title: 'How I Started',
    description:
      'I started my development journey by learning the fundamentals of web development, PHP, databases, and responsive design. Over time, I moved towards Laravel and modern frontend development with Vue.js.',
  },
  {
    number: '02',
    title: 'Professional Development',
    description:
      'Working on real business applications helped me understand database architecture, authentication, role-based access, REST APIs, server deployment, performance optimization, and maintainable code structure.',
  },
  {
    number: '03',
    title: 'What I Build Today',
    description:
      'Today, I develop full-stack web applications and mobile apps, including CRM systems, accounting software, custom product platforms, admin dashboards, order management systems, and real-time communication features.',
  },
]

const experiences = [
  {
    date: 'Jun 2026 — Present',
    company: 'Prosix',
    role: 'Full Stack Developer',
    location: 'Remote',
    description:
      'Developing business applications, sportswear customization platforms, CRM systems, mobile applications, REST APIs, real-time chat features, and internal management tools.',
    technologies: [
      'Laravel',
      'Vue.js',
      'Flutter',
      'MySQL',
    ],
  },
  {
    date: 'Jun 2025 — Jan 2026',
    company: 'Technology Brainz',
    role: 'WordPress Developer',
    location: 'Lahore',
    description:
      'Developed responsive WordPress websites, customized themes, worked with Elementor, improved website speed, handled maintenance, and delivered client-focused solutions.',
    technologies: [
      'WordPress',
      'PHP',
      'Elementor',
      'SEO',
    ],
  },
  {
    date: 'Aug 2023 — Jun 2025',
    company: 'Intelliage Solutions',
    role: 'Laravel Developer',
    location: 'Lahore',
    description:
      'Built Laravel web applications, developed REST APIs, managed databases, implemented authentication systems, fixed production issues, and improved application performance.',
    technologies: [
      'Laravel',
      'PHP',
      'MySQL',
      'REST API',
    ],
  },
]

const skillGroups = [
  {
    icon: '⚙',
    title: 'Backend Development',
    description:
      'Secure backend systems, business logic, authentication, APIs, and scalable database-driven applications.',
    skills: [
      'PHP',
      'Laravel',
      'Livewire',
      'REST API',
      'OOP',
      'MVC',
    ],
  },
  {
    icon: '◫',
    title: 'Frontend Development',
    description:
      'Responsive and user-friendly interfaces designed for modern browsers and multiple screen sizes.',
    skills: [
      'Vue.js',
      'JavaScript',
      'HTML5',
      'CSS3',
      'Bootstrap',
      'Tailwind CSS',
    ],
  },
  {
    icon: '▣',
    title: 'Mobile & Database',
    description:
      'Cross-platform mobile applications connected with secure APIs and optimized relational databases.',
    skills: [
      'Flutter',
      'Firebase',
      'MySQL',
      'SQLite',
      'FCM',
    ],
  },
  {
    icon: '⌘',
    title: 'Tools & Deployment',
    description:
      'Professional development workflow, version control, production deployment, and application maintenance.',
    skills: [
      'Git',
      'GitHub',
      'Ubuntu',
      'Nginx',
      'Vite',
      'Figma',
    ],
  },
]

const processSteps = [
  {
    icon: '◌',
    title: 'Understand',
    description:
      'I understand the business requirements, project goals, target users, and expected workflow.',
  },
  {
    icon: '✎',
    title: 'Plan',
    description:
      'I prepare the application structure, database flow, required modules, and development roadmap.',
  },
  {
    icon: '⌨',
    title: 'Develop',
    description:
      'I build the product using clean, maintainable code with a responsive and professional interface.',
  },
  {
    icon: '✓',
    title: 'Test & Launch',
    description:
      'I test functionality, fix issues, optimize performance, and deploy the application to production.',
  },
]

const values = [
  {
    icon: '✦',
    title: 'Clean & Maintainable Code',
    description:
      'Code is organized properly so future updates and new features can be added without unnecessary complexity.',
  },
  {
    icon: '⚡',
    title: 'Performance Focused',
    description:
      'Applications are optimized for speed, database efficiency, responsiveness, and a smooth user experience.',
  },
  {
    icon: '◉',
    title: 'Clear Communication',
    description:
      'I provide clear updates, discuss requirements honestly, and maintain transparency throughout development.',
  },
  {
    icon: '◆',
    title: 'Business-Oriented Solutions',
    description:
      'Every feature is built to solve a real problem and provide measurable value to the business.',
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
  --gold-dark: #d98b0b;
  --gold-soft: rgba(245, 166, 35, 0.12);
}

:global(html[data-theme='light']) {
  --bg-main: #f7f7f4;
  --bg-soft: #ffffff;
  --card-bg: #ffffff;
  --text-main: #111827;
  --text-muted: #5f6673;
  --border: #d8d8d8;
  --gold: #c88412;
  --gold-dark: #a96e0c;
  --gold-soft: rgba(200, 132, 18, 0.12);
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

.about-page {
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
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.section-label::before {
  width: 32px;
  height: 1px;
  background: var(--gold);
  content: '';
}

/* =========================
   HERO
========================= */

.about-hero {
  position: relative;
  display: flex;
  min-height: 100vh;
  align-items: center;
  padding: 145px 0 110px;
  overflow: hidden;
}

.trail-canvas {
  position: absolute;
  inset: 0;
  z-index: 2;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.hero-background {
  position: absolute;
  inset: 0;
  z-index: 0;
  overflow: hidden;
  background:
    radial-gradient(
      circle at 15% 25%,
      rgba(245, 166, 35, 0.1),
      transparent 28%
    ),
    radial-gradient(
      circle at 86% 70%,
      rgba(245, 166, 35, 0.07),
      transparent 28%
    );
  pointer-events: none;
}

.hero-background::before {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(
      rgba(255, 255, 255, 0.03) 1px,
      transparent 1px
    ),
    linear-gradient(
      90deg,
      rgba(255, 255, 255, 0.03) 1px,
      transparent 1px
    );
  background-size: 52px 52px;
  content: '';
  mask-image: radial-gradient(
    circle,
    #000 22%,
    transparent 82%
  );
}

.mouse-glow {
  position: absolute;
  width: 360px;
  height: 360px;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    rgba(245, 166, 35, 0.17),
    rgba(245, 166, 35, 0.055) 40%,
    transparent 72%
  );
  transform: translate(-50%, -50%);
  transition:
    left 0.08s linear,
    top 0.08s linear;
  filter: blur(4px);
}

.glow {
  position: absolute;
  border-radius: 50%;
  background: var(--gold);
  filter: blur(100px);
  opacity: 0.13;
  transition: transform 0.2s ease-out;
}

.glow-one {
  top: 8%;
  left: 2%;
  width: 310px;
  height: 310px;
}

.glow-two {
  right: 2%;
  bottom: 4%;
  width: 380px;
  height: 380px;
}

.floating-skill {
  position: absolute;
  padding: 7px 14px;
  border: 1px solid rgba(245, 166, 35, 0.24);
  border-radius: 100px;
  background: rgba(245, 166, 35, 0.07);
  color: var(--gold);
  font-family: monospace;
  font-size: 11px;
  backdrop-filter: blur(8px);
  transition: transform 0.16s ease-out;
  animation: floatingSkill 5s ease-in-out infinite;
}

.skill-one {
  top: 22%;
  left: 6%;
}

.skill-two {
  top: 33%;
  right: 7%;
  animation-delay: 1s;
}

.skill-three {
  right: 11%;
  bottom: 15%;
  animation-delay: 2s;
}

.skill-four {
  bottom: 12%;
  left: 10%;
  animation-delay: 3s;
}

.skill-five {
  top: 13%;
  right: 24%;
  animation-delay: 4s;
}

@keyframes floatingSkill {
  0%,
  100% {
    margin-top: 0;
  }

  50% {
    margin-top: -12px;
  }
}

.about-grid {
  position: relative;
  z-index: 3;
  display: grid;
  grid-template-columns: 0.92fr 1.08fr;
  align-items: center;
  gap: 90px;
}

/* =========================
   CIRCULAR PROFILE
========================= */

.image-column {
  display: flex;
  justify-content: center;
}

.profile-area {
  position: relative;
  width: 460px;
  height: 570px;
  transform-style: preserve-3d;
  transition: transform 0.18s ease-out;
}

.profile-circle-border {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 3;
  width: 410px;
  height: 410px;
  padding: 8px;
  border-radius: 50%;
  background:
    conic-gradient(
      from 0deg,
      transparent,
      var(--gold),
      transparent 35%,
      var(--gold) 60%,
      transparent 78%,
      var(--gold)
    );
  box-shadow:
    0 0 50px rgba(245, 166, 35, 0.15),
    0 35px 70px rgba(0, 0, 0, 0.36);
  transform: translate(-50%, -54%);
  animation: profileBorderRotate 9s linear infinite;
}

.profile-circle {
  width: 100%;
  height: 100%;
  padding: 7px;
  overflow: hidden;
  border: 2px solid var(--bg-main);
  border-radius: 50%;
  background: var(--bg-main);
  animation: profileImageCounterRotate 9s linear infinite;
}

.profile-image {
  display: block;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
  object-position: center 15%;
  transform: scale(1.03);
  transition: transform 0.4s ease;
}

.profile-area:hover .profile-image {
  transform: scale(1.08);
}

@keyframes profileBorderRotate {
  from {
    transform: translate(-50%, -54%) rotate(0deg);
  }

  to {
    transform: translate(-50%, -54%) rotate(360deg);
  }
}

@keyframes profileImageCounterRotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(-360deg);
  }
}

.profile-orbit {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 1;
  border: 1px solid rgba(245, 166, 35, 0.22);
  border-radius: 50%;
  transform: translate(-50%, -54%);
}

.profile-orbit span {
  position: absolute;
  display: block;
  width: 11px;
  height: 11px;
  border-radius: 50%;
  background: var(--gold);
  box-shadow: 0 0 18px rgba(245, 166, 35, 0.9);
}

.orbit-one {
  width: 450px;
  height: 450px;
  animation: orbitRotate 12s linear infinite;
}

.orbit-one span {
  top: 48px;
  right: 52px;
}

.orbit-two {
  width: 490px;
  height: 490px;
  border-style: dashed;
  opacity: 0.55;
  animation: orbitRotateReverse 17s linear infinite;
}

.orbit-two span {
  bottom: 70px;
  left: 24px;
}

@keyframes orbitRotate {
  from {
    transform: translate(-50%, -54%) rotate(0deg);
  }

  to {
    transform: translate(-50%, -54%) rotate(360deg);
  }
}

@keyframes orbitRotateReverse {
  from {
    transform: translate(-50%, -54%) rotate(360deg);
  }

  to {
    transform: translate(-50%, -54%) rotate(0deg);
  }
}

.profile-code {
  position: absolute;
  z-index: 6;
  display: flex;
  align-items: center;
  gap: 7px;
  padding: 9px 14px;
  border: 1px solid rgba(245, 166, 35, 0.26);
  border-radius: 100px;
  background: rgba(13, 17, 23, 0.9);
  color: #dce2e8;
  font-family: monospace;
  font-size: 11px;
  box-shadow: 0 14px 34px rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(12px);
}

.profile-code span {
  color: var(--gold);
}

.code-laravel {
  top: 65px;
  left: -2px;
  animation: codeFloat 4s ease-in-out infinite;
}

.code-vue {
  top: 145px;
  right: -20px;
  animation: codeFloat 4s ease-in-out infinite 1s;
}

.code-flutter {
  left: 15px;
  bottom: 115px;
  animation: codeFloat 4s ease-in-out infinite 2s;
}

@keyframes codeFloat {
  0%,
  100% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-9px);
  }
}

.experience-badge {
  position: absolute;
  right: -18px;
  bottom: 106px;
  z-index: 7;
  display: flex;
  min-width: 175px;
  align-items: center;
  gap: 12px;
  padding: 16px 18px;
  border: 1px solid rgba(245, 166, 35, 0.36);
  border-radius: 16px;
  background: rgba(13, 17, 23, 0.94);
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.36);
  backdrop-filter: blur(16px);
}

.experience-badge strong {
  color: var(--gold);
  font-size: 31px;
  font-weight: 900;
  line-height: 1;
}

.experience-badge span {
  display: block;
  color: #dde3e9;
  font-size: 10px;
  font-weight: 800;
  line-height: 1.4;
  text-transform: uppercase;
}

.availability-card {
  position: absolute;
  right: 45px;
  bottom: 22px;
  left: 45px;
  z-index: 8;
  display: flex;
  align-items: center;
  gap: 13px;
  padding: 15px 18px;
  border: 1px solid var(--border);
  border-radius: 14px;
  background: rgba(22, 27, 34, 0.95);
  box-shadow: 0 18px 42px rgba(0, 0, 0, 0.32);
  backdrop-filter: blur(15px);
}

.availability-dot {
  width: 10px;
  height: 10px;
  flex: 0 0 10px;
  border-radius: 50%;
  background: var(--gold);
  animation: statusPulse 1.8s infinite;
}

@keyframes statusPulse {
  0%,
  100% {
    box-shadow: 0 0 0 5px rgba(245, 166, 35, 0.12);
  }

  50% {
    box-shadow: 0 0 0 10px rgba(245, 166, 35, 0.02);
  }
}

.availability-card strong,
.availability-card small {
  display: block;
}

.availability-card strong {
  font-size: 13px;
}

.availability-card small {
  margin-top: 2px;
  color: var(--text-muted);
  font-size: 10px;
}

/* =========================
   HERO CONTENT
========================= */

.content-column h1 {
  max-width: 670px;
  margin: 0 0 25px;
  font-size: clamp(35px, 4vw, 57px);
  font-weight: 900;
  line-height: 1.05;
  letter-spacing: -2.5px;
}

.content-column h1 span {
  display: block;
  color: var(--gold);
}

.intro-text {
  margin-bottom: 16px;
  color: var(--text-main);
  font-size: 17px;
  line-height: 1.8;
}

.intro-text strong {
  color: var(--gold);
}

.description {
  margin-bottom: 14px;
  color: var(--text-muted);
  font-size: 14px;
  line-height: 1.9;
}

.quick-details {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 13px;
  margin-top: 30px;
}

.detail-item {
  display: flex;
  align-items: center;
  gap: 13px;
  padding: 14px;
  border: 1px solid var(--border);
  border-radius: 13px;
  background: rgba(255, 255, 255, 0.025);
  transition: 0.25s ease;
}

.detail-item:hover {
  transform: translateY(-3px);
  border-color: rgba(245, 166, 35, 0.45);
}

.detail-icon {
  display: flex;
  width: 38px;
  height: 38px;
  flex: 0 0 38px;
  align-items: center;
  justify-content: center;
  border-radius: 11px;
  background: var(--gold-soft);
  color: var(--gold);
  font-size: 16px;
}

.detail-item small,
.detail-item strong {
  display: block;
}

.detail-item small {
  margin-bottom: 2px;
  color: var(--text-muted);
  font-size: 9px;
  letter-spacing: 0.6px;
  text-transform: uppercase;
}

.detail-item strong {
  font-size: 11px;
}

.hero-actions,
.contact-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 13px;
  margin-top: 32px;
}

.primary-button,
.outline-button {
  display: inline-flex;
  min-height: 49px;
  align-items: center;
  justify-content: center;
  padding: 12px 28px;
  border: 1.5px solid var(--gold);
  border-radius: 10px;
  font-size: 13px;
  font-weight: 800;
  text-decoration: none;
  transition: 0.28s ease;
}

.primary-button {
  background: var(--gold);
  color: #0d1117;
  box-shadow: 0 12px 28px rgba(245, 166, 35, 0.16);
}

.primary-button:hover {
  transform: translateY(-3px);
  background: transparent;
  color: var(--gold);
  box-shadow: 0 0 26px rgba(245, 166, 35, 0.24);
}

.outline-button {
  border-color: var(--border);
  background: rgba(255, 255, 255, 0.025);
  color: var(--text-main);
}

.outline-button:hover {
  transform: translateY(-3px);
  border-color: var(--gold);
  background: var(--gold);
  color: #0d1117;
}

.scroll-indicator {
  position: absolute;
  bottom: 25px;
  left: 50%;
  z-index: 4;
  display: flex;
  align-items: center;
  gap: 9px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  transform: translateX(-50%);
}

.scroll-line {
  position: relative;
  width: 40px;
  height: 1px;
  overflow: hidden;
  background: var(--border);
}

.scroll-line::after {
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

/* =========================
   STATISTICS
========================= */

.numbers-section {
  position: relative;
  z-index: 4;
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background: var(--bg-soft);
}

.numbers-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}

.number-card {
  padding: 34px 24px;
  border-right: 1px solid var(--border);
  text-align: center;
  transition: 0.25s ease;
}

.number-card:last-child {
  border-right: none;
}

.number-card:hover {
  background: var(--gold-soft);
}

.number-value {
  color: var(--gold);
  font-size: 38px;
  font-weight: 900;
  line-height: 1;
}

.number-label {
  margin-top: 10px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 11px;
  letter-spacing: 0.7px;
  text-transform: uppercase;
}

/* =========================
   COMMON SECTIONS
========================= */

.section-heading {
  display: grid;
  grid-template-columns: 1fr 0.8fr;
  align-items: end;
  gap: 80px;
  margin-bottom: 58px;
}

.section-heading h2,
.center-heading h2 {
  max-width: 660px;
  margin: 0;
  font-size: clamp(31px, 4vw, 48px);
  font-weight: 900;
  line-height: 1.13;
  letter-spacing: -1.7px;
}

.section-heading > p,
.center-heading > p {
  margin: 0;
  color: var(--text-muted);
  font-size: 15px;
  line-height: 1.85;
}

.center-heading {
  max-width: 780px;
  margin: 0 auto 64px;
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
  margin: 0 auto 18px;
}

.center-heading p {
  max-width: 650px;
  margin: auto;
}

/* =========================
   STORY
========================= */

.story-section {
  background:
    radial-gradient(
      circle at 95% 10%,
      rgba(245, 166, 35, 0.06),
      transparent 30%
    );
}

.story-grid {
  display: grid;
  grid-template-columns: 1.05fr 0.95fr;
  align-items: center;
  gap: 70px;
}

.story-block {
  display: grid;
  grid-template-columns: 55px 1fr;
  gap: 20px;
  padding: 27px 0;
  border-bottom: 1px solid var(--border);
}

.story-block:first-child {
  padding-top: 0;
}

.story-number {
  color: var(--gold);
  font-family: monospace;
  font-size: 13px;
  font-weight: 800;
}

.story-block h3 {
  margin: 0 0 10px;
  font-size: 19px;
}

.story-block p {
  margin: 0;
  color: var(--text-muted);
  font-size: 14px;
  line-height: 1.85;
}

.code-card {
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 22px;
  background: #10141a;
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.25);
}

.code-card-header {
  display: flex;
  min-height: 52px;
  align-items: center;
  justify-content: space-between;
  padding: 0 19px;
  border-bottom: 1px solid #29303a;
  color: #7f8b99;
  font-family: monospace;
  font-size: 11px;
}

.window-buttons {
  display: flex;
  gap: 7px;
}

.window-buttons span {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.window-buttons span:nth-child(1) {
  background: #ff5f57;
}

.window-buttons span:nth-child(2) {
  background: #febc2e;
}

.window-buttons span:nth-child(3) {
  background: #28c840;
}

.code-content {
  padding: 36px 30px;
  overflow-x: auto;
  font-family: 'Courier New', monospace;
  font-size: 14px;
  line-height: 2;
}

.code-content p {
  min-width: max-content;
  margin: 0;
}

.code-indent {
  padding-left: 30px;
}

.code-purple {
  color: #c792ea;
}

.code-white {
  color: #d8dee9;
}

.code-blue {
  color: #82aaff;
}

.code-green {
  color: #c3e88d;
}

/* =========================
   TIMELINE
========================= */

.journey-section {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background: var(--bg-soft);
}

.timeline {
  position: relative;
  max-width: 960px;
  margin: auto;
}

.timeline::before {
  position: absolute;
  top: 10px;
  bottom: 10px;
  left: 151px;
  width: 1px;
  background: var(--border);
  content: '';
}

.timeline-item {
  position: relative;
  display: grid;
  grid-template-columns: 120px 32px 1fr;
  gap: 16px;
  margin-bottom: 30px;
}

.timeline-item:last-child {
  margin-bottom: 0;
}

.timeline-marker {
  position: relative;
  z-index: 2;
  display: flex;
  justify-content: center;
  padding-top: 29px;
}

.timeline-marker span {
  width: 13px;
  height: 13px;
  border: 3px solid var(--bg-soft);
  border-radius: 50%;
  background: var(--gold);
  box-shadow: 0 0 0 1px var(--gold);
}

.timeline-date {
  padding-top: 28px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 11px;
  text-align: right;
}

.timeline-card {
  padding: 26px;
  border: 1px solid var(--border);
  border-radius: 17px;
  background: var(--card-bg);
  transition: 0.28s ease;
}

.timeline-card:hover {
  transform: translateX(5px);
  border-color: rgba(245, 166, 35, 0.45);
}

.timeline-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 20px;
}

.timeline-card h3 {
  margin: 0;
  font-size: 18px;
}

.timeline-card h4 {
  margin: 4px 0 0;
  color: var(--gold);
  font-size: 13px;
}

.location-badge {
  padding: 5px 10px;
  border: 1px solid var(--border);
  border-radius: 100px;
  color: var(--text-muted);
  font-family: monospace;
  font-size: 10px;
}

.timeline-card > p {
  margin: 16px 0;
  color: var(--text-muted);
  font-size: 13px;
  line-height: 1.8;
}

.timeline-tags,
.skill-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.timeline-tags span,
.skill-list span {
  padding: 5px 10px;
  border: 1px solid rgba(245, 166, 35, 0.2);
  border-radius: 100px;
  background: var(--gold-soft);
  color: var(--gold);
  font-family: monospace;
  font-size: 10px;
}

/* =========================
   EXPERTISE
========================= */

.expertise-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 22px;
}

.expertise-card {
  padding: 28px;
  border: 1px solid var(--border);
  border-radius: 19px;
  background:
    linear-gradient(
      145deg,
      rgba(255, 255, 255, 0.035),
      rgba(255, 255, 255, 0.012)
    );
  transition: 0.28s ease;
}

.expertise-card:hover {
  transform: translateY(-5px);
  border-color: rgba(245, 166, 35, 0.48);
  box-shadow: 0 22px 44px rgba(0, 0, 0, 0.18);
}

.expertise-icon {
  display: flex;
  width: 48px;
  height: 48px;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  border-radius: 14px;
  background: var(--gold-soft);
  color: var(--gold);
  font-size: 20px;
}

.expertise-card h3 {
  margin: 0 0 9px;
  font-size: 18px;
}

.expertise-card > p {
  min-height: 72px;
  margin: 0 0 20px;
  color: var(--text-muted);
  font-size: 13px;
  line-height: 1.8;
}

/* =========================
   PROCESS
========================= */

.process-section {
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  background:
    radial-gradient(
      circle at 15% 85%,
      rgba(245, 166, 35, 0.06),
      transparent 28%
    ),
    var(--bg-soft);
}

.process-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 18px;
}

.process-card {
  position: relative;
  min-height: 280px;
  padding: 26px;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 18px;
  background: var(--card-bg);
  transition: 0.28s ease;
}

.process-card:hover {
  transform: translateY(-5px);
  border-color: rgba(245, 166, 35, 0.5);
}

.process-number {
  position: absolute;
  top: 10px;
  right: 16px;
  color: rgba(245, 166, 35, 0.09);
  font-size: 58px;
  font-weight: 900;
  line-height: 1;
}

.process-icon {
  display: flex;
  width: 44px;
  height: 44px;
  align-items: center;
  justify-content: center;
  margin-bottom: 44px;
  border-radius: 13px;
  background: var(--gold-soft);
  color: var(--gold);
  font-size: 19px;
}

.process-card h3 {
  margin: 0 0 10px;
  font-size: 17px;
}

.process-card p {
  margin: 0;
  color: var(--text-muted);
  font-size: 13px;
  line-height: 1.75;
}

/* =========================
   VALUES
========================= */

.values-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 18px;
}

.value-card {
  display: flex;
  align-items: flex-start;
  gap: 17px;
  padding: 24px;
  border: 1px solid var(--border);
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.02);
  transition: 0.25s ease;
}

.value-card:hover {
  transform: translateY(-4px);
  border-color: rgba(245, 166, 35, 0.45);
}

.value-icon {
  display: flex;
  width: 42px;
  height: 42px;
  flex: 0 0 42px;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  background: var(--gold-soft);
  color: var(--gold);
}

.value-card h3 {
  margin: 0 0 7px;
  font-size: 16px;
}

.value-card p {
  margin: 0;
  color: var(--text-muted);
  font-size: 13px;
  line-height: 1.75;
}

/* =========================
   CONTACT
========================= */

.contact-section {
  padding-top: 40px;
}

.contact-box {
  position: relative;
  padding: 75px 40px;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 28px;
  background:
    linear-gradient(
      145deg,
      rgba(245, 166, 35, 0.09),
      rgba(255, 255, 255, 0.018)
    );
  text-align: center;
}

.contact-glow {
  position: absolute;
  top: -140px;
  left: 50%;
  width: 380px;
  height: 280px;
  border-radius: 50%;
  background: var(--gold);
  filter: blur(120px);
  opacity: 0.12;
  transform: translateX(-50%);
}

.available-text {
  position: relative;
  display: inline-flex;
  align-items: center;
  gap: 9px;
  margin-bottom: 22px;
  color: var(--gold);
  font-family: monospace;
  font-size: 11px;
  letter-spacing: 0.8px;
  text-transform: uppercase;
}

.available-text span {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: var(--gold);
  animation: statusPulse 1.8s infinite;
}

.contact-box h2 {
  position: relative;
  max-width: 750px;
  margin: 0 auto 15px;
  font-size: clamp(34px, 5vw, 54px);
  font-weight: 900;
  line-height: 1.12;
  letter-spacing: -1.8px;
}

.contact-box > p {
  position: relative;
  max-width: 660px;
  margin: auto;
  color: var(--text-muted);
  font-size: 15px;
  line-height: 1.85;
}

.contact-actions {
  position: relative;
  justify-content: center;
}

/* =========================
   FOOTER
========================= */

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
  font-size: 11px;
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 1050px) {
  .about-grid {
    grid-template-columns: 0.9fr 1.1fr;
    gap: 55px;
  }

  .profile-area {
    width: 410px;
    height: 530px;
  }

  .profile-circle-border {
    width: 365px;
    height: 365px;
  }

  .orbit-one {
    width: 405px;
    height: 405px;
  }

  .orbit-two {
    width: 440px;
    height: 440px;
  }

  .content-column h1 {
    font-size: 50px;
  }

  .process-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 850px) {
  .about-hero {
    padding-top: 130px;
  }

  .about-grid,
  .story-grid,
  .section-heading {
    grid-template-columns: 1fr;
  }

  .about-grid {
    gap: 65px;
  }

  .content-column {
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

  .content-column h1,
  .description {
    margin-right: auto;
    margin-left: auto;
  }

  .hero-actions {
    justify-content: center;
  }

  .image-column {
    margin-top: 10px;
  }

  .section-heading {
    gap: 20px;
  }

  .timeline::before {
    left: 131px;
  }

  .timeline-item {
    grid-template-columns: 100px 32px 1fr;
  }

  .numbers-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .number-card:nth-child(2) {
    border-right: none;
  }

  .number-card:nth-child(-n + 2) {
    border-bottom: 1px solid var(--border);
  }
}

@media (max-width: 640px) {
  .container {
    padding: 0 18px;
  }

  .section {
    padding: 75px 0;
  }

  .about-hero {
    min-height: auto;
    padding: 115px 0 75px;
  }

  .floating-skill,
  .scroll-indicator {
    display: none;
  }

  .content-column h1 {
    font-size: 38px;
    letter-spacing: -1.5px;
  }

  .intro-text {
    font-size: 15px;
  }

  .quick-details,
  .expertise-grid,
  .values-grid,
  .process-grid {
    grid-template-columns: 1fr;
  }

  .detail-item {
    text-align: left;
  }

  .hero-actions,
  .contact-actions {
    flex-direction: column;
  }

  .primary-button,
  .outline-button {
    width: 100%;
  }

  .profile-area {
    width: 340px;
    height: 455px;
  }

  .profile-circle-border {
    width: 305px;
    height: 305px;
  }

  .orbit-one {
    width: 335px;
    height: 335px;
  }

  .orbit-two {
    width: 365px;
    height: 365px;
  }

  .profile-code {
    padding: 7px 10px;
    font-size: 9px;
  }

  .code-laravel {
    top: 50px;
    left: -5px;
  }

  .code-vue {
    top: 110px;
    right: -8px;
  }

  .code-flutter {
    bottom: 100px;
    left: 0;
  }

  .experience-badge {
    right: -5px;
    bottom: 88px;
    min-width: 145px;
    padding: 12px 14px;
  }

  .experience-badge strong {
    font-size: 25px;
  }

  .experience-badge span {
    font-size: 8px;
  }

  .availability-card {
    right: 20px;
    bottom: 12px;
    left: 20px;
  }

  .numbers-grid {
    grid-template-columns: 1fr 1fr;
  }

  .number-card {
    padding: 27px 12px;
  }

  .number-value {
    font-size: 31px;
  }

  .section-heading h2,
  .center-heading h2 {
    font-size: 34px;
  }

  .story-block {
    grid-template-columns: 40px 1fr;
    gap: 12px;
  }

  .code-content {
    padding: 26px 18px;
    font-size: 12px;
  }

  .timeline::before {
    left: 6px;
  }

  .timeline-item {
    grid-template-columns: 14px 1fr;
    gap: 14px;
  }

  .timeline-marker {
    grid-column: 1;
    grid-row: 1 / span 2;
    justify-content: flex-start;
    padding-top: 6px;
  }

  .timeline-date {
    grid-column: 2;
    padding-top: 0;
    text-align: left;
  }

  .timeline-card {
    grid-column: 2;
    padding: 21px;
  }

  .timeline-top {
    flex-direction: column;
    gap: 10px;
  }

  .expertise-card > p {
    min-height: 0;
  }

  .contact-box {
    padding: 52px 22px;
  }

  .contact-box h2 {
    font-size: 35px;
  }

  .footer-inner {
    flex-direction: column;
    text-align: center;
  }
}

@media (max-width: 390px) {
  .content-column h1 {
    font-size: 33px;
  }

  .profile-area {
    width: 300px;
    height: 415px;
  }

  .profile-circle-border {
    width: 270px;
    height: 270px;
  }

  .orbit-one {
    width: 295px;
    height: 295px;
  }

  .orbit-two {
    width: 320px;
    height: 320px;
  }

  .profile-code {
    display: none;
  }

  .numbers-grid {
    grid-template-columns: 1fr;
  }

  .number-card {
    border-right: none;
    border-bottom: 1px solid var(--border);
  }

  .number-card:last-child {
    border-bottom: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  .profile-circle-border,
  .profile-circle,
  .profile-orbit,
  .profile-code,
  .floating-skill,
  .scroll-line::after {
    animation: none;
  }

  .profile-area,
  .floating-skill,
  .glow {
    transform: none !important;
  }
}
</style>

<template>
  <div class="projects-page">
    <nav-component />

    <section ref="heroSection" class="projects-hero" @mousemove="handleMouseMove" @mouseleave="resetMouse">
      <canvas ref="trailCanvas" class="trail-canvas"></canvas>
      <div class="hero-bg">
        <span class="hero-glow glow-one" :style="{ transform: `translate3d(${mouse.x * 25}px, ${mouse.y * 25}px, 0)` }"></span>
        <span class="hero-glow glow-two" :style="{ transform: `translate3d(${mouse.x * -30}px, ${mouse.y * -30}px, 0)` }"></span>
        <span class="floating-word word-one">Laravel</span><span class="floating-word word-two">Vue.js</span><span class="floating-word word-three">Flutter</span>
      </div>
      <div class="container hero-content">
        <div class="section-label">Portfolio Projects</div>
        <h1>Real products built for <span>real business needs.</span></h1>
        <p>I design and develop complete web and mobile products—from business workflows and dashboards to eCommerce, customizers, Flutter applications, APIs, real-time communication, and production deployment.</p>
        <div class="hero-actions"><a href="#project-showcase" class="btn-primary">Explore Projects</a><a href="mailto:itbilal73@gmail.com" class="btn-outline">Start a Project</a></div>
        <div class="hero-stats"><article><strong>{{ projects.length }}+</strong><span>Featured Projects</span></article><article><strong>{{ projects.filter(p => p.portfolioGroup === 'live').length }}</strong><span>Live Projects</span></article><article><strong>Full Stack</strong><span>Design to Deployment</span></article></div>
      </div>
    </section>

    <section id="project-showcase" class="section showcase-section">
      <div class="container">
        <div class="section-heading"><div><div class="section-label">Selected Work</div><h2>Projects that show how I solve problems.</h2></div><p>Each project combines clean user experience, maintainable code, responsive design, secure workflows, and practical business functionality.</p></div>
        <div class="filter-bar">
          <button v-for="filter in filters" :key="filter.value" type="button" :class="{ active: activeFilter === filter.value }" @click="activeFilter = filter.value">{{ filter.label }} <span>{{ countByFilter(filter.value) }}</span></button>
        </div>
        <TransitionGroup name="project-list" tag="div" class="projects-grid">
          <article v-for="project in filteredProjects" :key="project.slug" class="project-card" :class="{ featured: project.featured, 'mobile-project-card': project.isMobile }">
            <div
              class="thumbnail-wrap"
              :class="{ 'mobile-thumbnail-wrap': project.isMobile }"
              role="button"
              tabindex="0"
              :aria-label="`Open ${project.name} image`"
              @click="openImage(project)"
              @keydown.enter="openImage(project)"
              @keydown.space.prevent="openImage(project)"
            >
              <img
                :src="project.thumbnail"
                :alt="`${project.name} project thumbnail`"
                class="project-thumbnail"
                :class="{ 'mobile-project-thumbnail': project.isMobile }"
              />

              <div class="thumbnail-overlay">
                <span>{{ project.type }}</span>
                <button type="button" class="view-image-btn" @click.stop="openImage(project)">
                  View Full Image ↗
                </button>
              </div>

              <span v-if="project.featured" class="featured-badge">Featured</span>
              <span class="project-number">{{ project.number }}</span>
            </div>
            <div class="project-content">
              <div class="project-topline"><span>{{ project.category }}</span><span>{{ project.year }}</span></div>
              <h3>{{ project.name }}</h3><p>{{ project.shortDescription }}</p>
              <div class="project-results"><span v-for="result in project.results" :key="result">✓ {{ result }}</span></div>
              <div class="project-tags"><span v-for="technology in project.technologies" :key="technology">{{ technology }}</span></div>
              <div class="project-actions"><a v-if="project.liveUrl" :href="project.liveUrl" target="_blank" rel="noopener" class="project-primary">Live Project ↗</a><button v-else-if="project.isMobile" type="button" class="project-primary" @click="openImage(project)">View App Screens</button><button type="button" class="project-secondary" @click="openProject(project)">Project Details</button></div>
            </div>
          </article>
        </TransitionGroup>
      </div>
    </section>

    <section class="section process-section"><div class="container"><div class="center-heading"><div class="section-label">How I Build</div><h2>Every project follows a professional workflow.</h2><p>Clear planning and structured development help me deliver products that are reliable, scalable, and easier to maintain.</p></div><div class="process-grid"><article v-for="(step,index) in process" :key="step.title"><span class="process-number">{{ String(index + 1).padStart(2, '0') }}</span><span class="process-icon">{{ step.icon }}</span><h3>{{ step.title }}</h3><p>{{ step.description }}</p></article></div></div></section>

    <section class="section contact-section"><div class="container"><div class="contact-box"><div class="availability"><span></span>Available for freelance and remote projects</div><h2>Have a project that needs a strong full-stack developer?</h2><p>Share your idea, existing website, or business workflow. I can help you plan, rebuild, improve, and deploy a professional solution.</p><div class="contact-actions"><a href="mailto:itbilal73@gmail.com" class="btn-primary">Discuss Your Project</a><a href="tel:03015825174" class="btn-outline">Call: 0301-5825174</a></div></div></div></section>

    <div v-if="selectedProject" class="project-modal" @click.self="closeProject">
      <div class="modal-card">
        <button class="modal-close" type="button" @click="closeProject">×</button>
        <div class="modal-image-stage" :class="{ 'mobile-modal-stage': selectedProject.isMobile }"><img :src="selectedProject.thumbnail" :alt="selectedProject.name" :class="{ 'mobile-modal-image': selectedProject.isMobile }" /></div>
        <div class="modal-body">
          <div class="section-label">{{ selectedProject.type }}</div>
          <h2>{{ selectedProject.name }}</h2>
          <p>{{ selectedProject.fullDescription }}</p>
          <div class="modal-features">
            <span v-for="feature in selectedProject.features" :key="feature">✓ {{ feature }}</span>
          </div>
          <div class="project-tags">
            <span v-for="technology in selectedProject.technologies" :key="technology">{{ technology }}</span>
          </div>
          <a v-if="selectedProject.liveUrl" :href="selectedProject.liveUrl" target="_blank" rel="noopener" class="btn-primary">
            Visit Live Project ↗
          </a>
        </div>
      </div>
    </div>

    <div v-if="imagePreview" class="image-lightbox" @click.self="closeImage">
      <div class="image-lightbox-card">
        <div class="image-lightbox-header">
          <div>
            <span>{{ imagePreview.type }}</span>
            <h3>{{ imagePreview.name }}</h3>
          </div>
          <button type="button" class="image-lightbox-close" @click="closeImage">×</button>
        </div>

        <div class="image-lightbox-body" :class="{ 'mobile-lightbox-body': imagePreview.isMobile }">
          <div v-if="imagePreview.isMobile" class="phone-preview-frame">
            <div class="phone-speaker"></div>
            <img :src="imagePreview.thumbnail" :alt="`${imagePreview.name} mobile preview`" />
            <div class="phone-home-indicator"></div>
          </div>
          <img v-else :src="imagePreview.thumbnail" :alt="`${imagePreview.name} full preview`" />
        </div>

        <div class="image-lightbox-footer">
          <button type="button" class="project-secondary" @click="showProjectFromImage">
            Project Details
          </button>
          <a
            v-if="imagePreview.liveUrl"
            :href="imagePreview.liveUrl"
            target="_blank"
            rel="noopener"
            class="project-primary"
          >
            Open Live Website ↗
          </a>
        </div>
      </div>
    </div>

    <footer class="footer"><div class="container footer-inner"><span>© 2026 Muhammad Bilal — Full-Stack Developer</span><span>Laravel · Vue.js · Flutter · MySQL</span></div></footer>
  </div>
</template>

<script setup>
import { computed, onBeforeUnmount, onMounted, reactive, ref } from 'vue'
const heroSection=ref(null), trailCanvas=ref(null), activeFilter=ref('all'), selectedProject=ref(null), imagePreview=ref(null), mouse=reactive({x:0,y:0})
let context=null, frame=null, particles=[]
const filters=[{label:'All Projects',value:'all'},{label:'Live',value:'live'},{label:'Web Apps',value:'web'},{label:'Mobile',value:'mobile'},{label:'Personal',value:'personal'}]
const projects=[
{
  number:'01',slug:'prosix-sports',name:'Prosix Sports',category:'Sportswear eCommerce',type:'Live Client Website',portfolioGroup:'live',year:'2026',featured:true,
  liveUrl:'https://prosix.com',thumbnail:'/assets/images/projects/prosix-sports.webp',
  shortDescription:'A modern sportswear business website built to showcase custom uniforms, products, services, and customer inquiries.',
  fullDescription:'Prosix Sports is a production-ready sportswear website designed for international clients. It presents custom teamwear, product categories, services, and inquiry options through a clean, responsive, conversion-focused experience.',
  technologies:['Laravel','Vue.js','MySQL','Responsive UI'],
  results:['Professional brand presentation','Responsive customer experience','Live production deployment'],
  features:['Product and category pages','Custom sportswear presentation','Inquiry and contact workflows','Mobile-first responsive design']
},
{
  number:'06',slug:'medexcore',name:'Medexcore',category:'Healthcare Technology Website',type:'Live Client Website',portfolioGroup:'live',year:'2026',featured:false,
  liveUrl:'https://medexcore.com',thumbnail:'/assets/images/projects/medexcore.webp',
  shortDescription:'A professional healthcare technology website designed to communicate services, credibility, solutions, and business value clearly.',
  fullDescription:'Medexcore is a live healthcare-focused business website with a clean and trustworthy visual direction. The site presents company solutions, service information, brand credibility, and conversion-focused contact paths for professional audiences.',
  technologies:['Laravel','Vue.js','Responsive UI','SEO'],
  results:['Professional healthcare branding','Trust-focused interface','Live responsive deployment'],
  features:['Service and solution pages','Professional business presentation','Responsive layouts','Contact and inquiry workflow']
},

{
  number:'03',slug:'ai-blogmatic',name:'AI Blogmatic',category:'AI Content SaaS',type:'Live Client Website',portfolioGroup:'live',year:'2026',featured:true,
  liveUrl:'https://aiblogmatic.com',thumbnail:'/assets/images/projects/ai-blogmatic.webp',
  shortDescription:'An AI-powered content platform for generating SEO-friendly blogs, articles, and marketing content through a polished SaaS interface.',
  fullDescription:'AI Blogmatic is a live SaaS-style website designed around AI-assisted content creation. The product presents automated blog generation, SEO-focused writing, user workflows, and a modern interface suitable for marketers and content teams.',
  technologies:['Laravel','Vue.js','AI Integration','MySQL','SEO'],
  results:['Live SaaS experience','SEO-focused content workflow','Modern responsive interface'],
  features:['AI content generation workflow','Blog and article tools','User-friendly dashboard experience','Responsive landing pages','SEO-oriented presentation']
},
{
  number:'04',slug:'mr-furniture-usa',name:'Mr Furniture USA',category:'Furniture eCommerce',type:'Live USA Client Website',portfolioGroup:'live',year:'2026',featured:true,
  liveUrl:'https://mrfurnitureusa.com',thumbnail:'/assets/images/projects/mr-furniture-usa.webp',
  shortDescription:'A complete furniture shopping website for a USA-based business with categories, product listings, offers, and responsive shopping pages.',
  fullDescription:'Mr Furniture USA is a live eCommerce website created for an American furniture business. It includes structured furniture categories, product collections, promotional pricing, detailed product pages, and a responsive customer shopping experience.',
  technologies:['Laravel','Vue.js','MySQL','eCommerce','Responsive UI'],
  results:['USA client delivery','Large product catalog','Live eCommerce deployment'],
  features:['Furniture categories and collections','Product listing and detail pages','Promotional pricing','Responsive shopping experience','Admin-managed catalog']
},
{
  number:'05',slug:'pakistan-cooling',name:'Pakistan Cooling Center',category:'Home Services Website',type:'Live Client Website',portfolioGroup:'live',year:'2026',featured:false,
  liveUrl:'https://pakistancooling.com',thumbnail:'/assets/images/projects/pakistan-cooling.webp',
  shortDescription:'A service-focused website for appliance repair, including AC, refrigerator, washing machine, microwave, and maintenance services.',
  fullDescription:'Pakistan Cooling Center is a live local-services website built to generate customer calls and inquiries. It presents appliance repair services, trust-focused information, service pages, and clear mobile contact actions.',
  technologies:['Laravel','Vue.js','SEO','Responsive UI'],
  results:['Service-focused conversion','Mobile call experience','Search-friendly page structure'],
  features:['Dedicated service pages','Call and inquiry actions','Responsive layout','Local business presentation','SEO-ready content structure']
},
{
  number:'02',slug:'prosix-customizer',name:'Prosix Product Customizer',category:'Interactive Web Application',type:'Live Client Web App',portfolioGroup:'live',year:'2026',featured:true,
  liveUrl:'https://customizer.prosix.com/category/59/products',thumbnail:'/assets/images/projects/prosix-customizer.webp',
  shortDescription:'An advanced apparel customization platform with real-time colors, text, fonts, patterns, mascots, and multi-view previews.',
  fullDescription:'A complete browser-based product customizer for personalized sportswear. Customers can edit multiple garment views, apply team colors, names, numbers, fonts, patterns, and mascots, then save and preview their designs.',
  technologies:['Laravel','Vue.js','JavaScript','SVG','Canvas'],
  results:['Real-time product editing','Complex SVG workflow','Multi-view design synchronization'],
  features:['Front, back, left and right views','SVG color mapping','Text, font and number tools','Pattern and mascot controls','Saved design previews']
},

{
  number:'07',slug:'od-shop',name:'OD Shop',category:'Online Store',type:'Live eCommerce Project',portfolioGroup:'live',year:'2026',featured:false,
  liveUrl:'https://odshop.com',thumbnail:'/assets/images/projects/od-shop.webp',
  shortDescription:'An online shopping project designed with product discovery, catalog browsing, responsive layouts, and customer-focused purchasing flows.',
  fullDescription:'OD Shop is presented as an eCommerce project focused on a clean catalog experience, product browsing, responsive pages, and practical online-store workflows. Confirm the public domain is displaying the completed website before publishing this portfolio entry.',
  technologies:['Laravel','Vue.js','MySQL','eCommerce'],
  results:['Responsive store structure','Product-focused user journey','Deployment-ready workflow'],
  features:['Product catalog','Category browsing','Responsive storefront','Shopping and order workflow']
},
{
  number:'08',slug:'prosix-crm',name:'Prosix CRM Workspace',category:'CRM & Order Management',type:'Personal / Internal Project',portfolioGroup:'personal',year:'2026',featured:true,
  liveUrl:'https://crm.prosix.com',thumbnail:'/assets/images/projects/prosix-crm.webp',
  shortDescription:'A role-based business workspace with orders, team members, files, invoices, tracking, payments, chat, and notifications.',
  fullDescription:'A complete internal CRM and production workspace built for Prosix operations. It centralizes customer orders, assigned staff, production files, invoices, tracking information, payments, notes, and real-time communication in one secure system.',
  technologies:['Laravel','Vue.js','Sanctum','Reverb','MySQL'],
  results:['Centralized order operations','Role-based team access','Real-time collaboration'],
  features:['Order and member management','Real-time chat and read receipts','Files, invoices and notes','Tracking and payment details','Client and staff permissions']
},
{
  number:'09',slug:'prosix-accounts',name:'Prosix Accounts & Payroll',category:'Factory Management System',type:'Personal / Internal Project',portfolioGroup:'personal',year:'2026',featured:true,
  liveUrl:'https://accounts.prosix.com',thumbnail:'/assets/images/projects/prosix-accounts.webp',
  shortDescription:'A factory accounts and payroll system for employees, attendance, salary, advances, expenses, contractors, and reports.',
  fullDescription:'A custom internal management platform created for factory operations. It handles employee records, biometric and manual attendance, payroll calculations, salary advances, expenses, contractor bills, monthly alerts, payment status, and printable salary reports.',
  technologies:['Laravel','Blade','MySQL','Bootstrap','Biometric'],
  results:['Automated salary calculations','Centralized employee records','Printable operational reports'],
  features:['Employee and department management','Attendance and payroll','Salary advances and payment status','Expense and contractor modules','Reports and printable slips']
},
,
{
  number:'10',
  slug:'prosix-sports-mobile',
  name:'Prosix Sports Mobile App',
  category:'Mobile Application',
  type:'Flutter Mobile App',
  portfolioGroup:'personal',
  year:'2026',
  featured:true,
  liveUrl:null,
  thumbnail:'/assets/images/projects/prosix-sports-mobile.png',
  isMobile:true,
  shortDescription:'A modern sportswear mobile application for browsing products, viewing categories, exploring custom uniforms, and contacting the business.',
  fullDescription:'Prosix Sports Mobile App is a Flutter-based mobile experience designed for customers who want to explore sportswear products and custom team uniform services from their phones. The application focuses on fast navigation, clean product presentation, responsive screens, and a professional brand experience.',
  technologies:['Flutter','Laravel API','Firebase','REST API'],
  results:['Native mobile experience','Fast product browsing','Professional sportswear presentation'],
  features:['Product and category browsing','Custom uniform presentation','Customer inquiry workflow','Responsive mobile screens','API-connected architecture']
},
{
  number:'11',
  slug:'prosix-order-management-mobile',
  name:'Prosix Order Management App',
  category:'Mobile Application',
  type:'Flutter Business App',
  portfolioGroup:'personal',
  year:'2026',
  featured:true,
  liveUrl:null,
  thumbnail:'/assets/images/projects/prosix-order-management-mobile.webp',
  isMobile:true,
  shortDescription:'A complete mobile order-management application with orders, team members, files, notes, chat, notifications, tracking, and payment information.',
  fullDescription:'Prosix Order Management App is a Flutter business application connected to the Prosix CRM Laravel API. It allows authorized staff to manage orders, view assigned work, communicate through chat, open files, check invoices, track payments, receive notifications, and work from mobile devices.',
  technologies:['Flutter','Laravel API','Firebase','Reverb','REST API'],
  results:['Mobile production workflow','Real-time team communication','Role-based business access'],
  features:['Order and status management','Real-time chat and notifications','Files and invoice previews','Tracking and payment details','Member permissions and profiles']
},
{
  number:'12',
  slug:'prosix-workforce-mobile',
  name:'Prosix Workforce Mobile App',
  category:'Mobile Application',
  type:'Flutter Team App',
  portfolioGroup:'personal',
  year:'2026',
  featured:false,
  liveUrl:null,
  thumbnail:'/assets/images/projects/prosix-workforce-mobile.webp',
  isMobile:true,
  shortDescription:'A workforce-focused mobile application for employee tasks, work updates, team activity, notifications, files, and operational communication.',
  fullDescription:'Prosix Workforce Mobile App is a Flutter application concept created for staff and operational teams. It provides secure login, assigned work, order updates, team communication, notifications, file access, profile management, and an API-driven workflow designed for daily business use.',
  technologies:['Flutter','Laravel API','Firebase','SQLite'],
  results:['Cross-platform workforce access','API-driven architecture','Notification-ready workflow'],
  features:['Secure authentication','Assigned work and updates','Team chat and notifications','File previews and uploads','Profile and activity management']
}

]
const filteredProjects=computed(()=>projects.filter(p=>activeFilter.value==='all'||(activeFilter.value==='live'&&p.portfolioGroup==='live')||(activeFilter.value==='personal'&&p.portfolioGroup==='personal')||(activeFilter.value==='mobile'&&p.category==='Mobile Application')||(activeFilter.value==='web'&&p.category!=='Mobile Application')))
const countByFilter=v=>v==='all'?projects.length:v==='live'?projects.filter(p=>p.portfolioGroup==='live').length:v==='personal'?projects.filter(p=>p.portfolioGroup==='personal').length:v==='mobile'?projects.filter(p=>p.category==='Mobile Application').length:projects.filter(p=>p.category!=='Mobile Application').length
const process=[{icon:'◌',title:'Discovery',description:'I understand business goals, users, workflows, requirements, and the current problems to solve.'},{icon:'✎',title:'Planning & UI',description:'I plan architecture, database flow, modules, responsive layouts, and the complete user journey.'},{icon:'⌨',title:'Development',description:'I build secure backend logic, polished interfaces, integrations, APIs, and required automation.'},{icon:'✓',title:'Testing & Launch',description:'I test permissions, responsiveness, workflows, edge cases, performance, and production deployment.'}]
const openProject=p=>{
  selectedProject.value=p
  document.body.style.overflow='hidden'
}

const closeProject=()=>{
  selectedProject.value=null
  if(!imagePreview.value) document.body.style.overflow=''
}

const openImage=p=>{
  imagePreview.value=p
  document.body.style.overflow='hidden'
}

const closeImage=()=>{
  imagePreview.value=null
  if(!selectedProject.value) document.body.style.overflow=''
}

const showProjectFromImage=()=>{
  const project=imagePreview.value
  imagePreview.value=null
  if(project) selectedProject.value=project
}

const handleEscape=e=>{
  if(e.key!=='Escape') return
  if(imagePreview.value){
    closeImage()
    return
  }
  if(selectedProject.value) closeProject()
}
const resizeCanvas=()=>{const c=trailCanvas.value;if(!c)return;const r=c.getBoundingClientRect(),d=window.devicePixelRatio||1;c.width=r.width*d;c.height=r.height*d;c.style.width=`${r.width}px`;c.style.height=`${r.height}px`;context=c.getContext('2d');context?.setTransform(d,0,0,d,0,0)}
const handleMouseMove=e=>{const s=heroSection.value;if(!s)return;const r=s.getBoundingClientRect(),x=e.clientX-r.left,y=e.clientY-r.top;mouse.x=x/r.width-.5;mouse.y=y/r.height-.5;for(let i=0;i<3;i++)particles.push({x,y,vx:(Math.random()-.5)*1.8,vy:(Math.random()-.5)*1.8,size:Math.random()*2+1,life:1});if(particles.length>120)particles=particles.slice(-120)}
const resetMouse=()=>{mouse.x=0;mouse.y=0}
const animate=()=>{const c=trailCanvas.value;if(!c||!context){frame=requestAnimationFrame(animate);return}const r=c.getBoundingClientRect();context.clearRect(0,0,r.width,r.height);particles.forEach(p=>{p.x+=p.vx;p.y+=p.vy;p.life-=.02;context.beginPath();context.arc(p.x,p.y,p.size,0,Math.PI*2);context.fillStyle=`rgba(245,166,35,${Math.max(p.life,0)})`;context.shadowBlur=14;context.shadowColor='#f5a623';context.fill()});particles=particles.filter(p=>p.life>0);frame=requestAnimationFrame(animate)}
onMounted(()=>{resizeCanvas();window.addEventListener('resize',resizeCanvas);window.addEventListener('keydown',handleEscape);frame=requestAnimationFrame(animate)})
onBeforeUnmount(()=>{window.removeEventListener('resize',resizeCanvas);window.removeEventListener('keydown',handleEscape);if(frame)cancelAnimationFrame(frame);document.body.style.overflow=''})
</script>

<style scoped>
:global(:root){--bg-main:#0d1117;--bg-soft:#151a21;--card-bg:#161b22;--text-main:#e6edf3;--text-muted:#9aa4b2;--border:#2f3742;--gold:#f5a623;--gold-dark:#d98b0b;--gold-soft:rgba(245,166,35,.12)}
:global(html[data-theme='light']){--bg-main:#f8f7f2;--bg-soft:#fff;--card-bg:#fff;--text-main:#111827;--text-muted:#626a76;--border:#ddd9cf;--gold:#c88412;--gold-dark:#a96e0c;--gold-soft:rgba(200,132,18,.12)}
*{box-sizing:border-box}.projects-page{min-height:100vh;overflow:hidden;background:var(--bg-main);color:var(--text-main);font-family:'Inter',system-ui,sans-serif;line-height:1.6}.container{width:100%;max-width:1180px;margin:auto;padding:0 24px}.section{padding:105px 0}.section-label{display:inline-flex;align-items:center;gap:10px;margin-bottom:16px;color:var(--gold);font:700 12px monospace;letter-spacing:2px;text-transform:uppercase}.section-label:before{content:'';width:32px;height:1px;background:var(--gold)}
.projects-hero{position:relative;min-height:92vh;display:flex;align-items:center;padding:150px 0 100px;overflow:hidden}.trail-canvas{position:absolute;inset:0;z-index:2;width:100%;height:100%;pointer-events:none}.hero-bg{position:absolute;inset:0;overflow:hidden;background:radial-gradient(circle at 18% 24%,var(--gold-soft),transparent 30%),linear-gradient(rgba(255,255,255,.025) 1px,transparent 1px),linear-gradient(90deg,rgba(255,255,255,.025) 1px,transparent 1px);background-size:auto,54px 54px,54px 54px}.hero-glow{position:absolute;width:360px;height:360px;border-radius:50%;background:var(--gold);filter:blur(100px);opacity:.12;transition:transform .15s ease}.glow-one{right:8%;top:12%}.glow-two{left:5%;bottom:5%}.floating-word{position:absolute;color:var(--gold);font:700 12px monospace;letter-spacing:2px;opacity:.4}.word-one{left:8%;top:30%}.word-two{right:10%;top:34%}.word-three{right:20%;bottom:16%}.hero-content{position:relative;z-index:3;text-align:center;max-width:920px}.hero-content h1{font-size:clamp(48px,7vw,88px);line-height:1.02;letter-spacing:-4px;margin:0 0 25px}.hero-content h1 span{color:var(--gold)}.hero-content>p{max-width:780px;margin:0 auto;color:var(--text-muted);font-size:18px}.hero-actions,.contact-actions{display:flex;justify-content:center;gap:14px;flex-wrap:wrap;margin-top:34px}.btn-primary,.btn-outline{display:inline-flex;align-items:center;justify-content:center;padding:13px 25px;border-radius:9px;font-weight:800;text-decoration:none;transition:.25s}.btn-primary{background:var(--gold);color:#111;border:1px solid var(--gold)}.btn-primary:hover{background:var(--gold-dark);transform:translateY(-2px)}.btn-outline{color:var(--text-main);border:1px solid var(--border);background:transparent}.btn-outline:hover{border-color:var(--gold);color:var(--gold);transform:translateY(-2px)}.hero-stats{display:grid;grid-template-columns:repeat(3,1fr);max-width:760px;margin:58px auto 0;border:1px solid var(--border);border-radius:16px;background:rgba(22,27,34,.7);backdrop-filter:blur(14px)}.hero-stats article{padding:22px;border-right:1px solid var(--border)}.hero-stats article:last-child{border:0}.hero-stats strong{display:block;font-size:22px;color:var(--gold)}.hero-stats span{color:var(--text-muted);font-size:12px;text-transform:uppercase;letter-spacing:1px}
.showcase-section{background:var(--bg-soft)}.section-heading{display:grid;grid-template-columns:1.1fr .9fr;align-items:end;gap:60px;margin-bottom:42px}.section-heading h2,.center-heading h2{font-size:clamp(34px,5vw,54px);line-height:1.12;letter-spacing:-2px;margin:0}.section-heading>p,.center-heading>p{color:var(--text-muted);margin:0}.filter-bar{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:34px}.filter-bar button{border:1px solid var(--border);background:var(--card-bg);color:var(--text-muted);padding:10px 15px;border-radius:999px;font-weight:700;cursor:pointer;transition:.2s}.filter-bar button span{display:inline-grid;place-items:center;min-width:22px;height:22px;margin-left:7px;border-radius:50%;background:var(--bg-main);font-size:11px}.filter-bar button:hover,.filter-bar button.active{background:var(--gold);border-color:var(--gold);color:#111}.projects-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:26px}.project-card{border:1px solid var(--border);border-radius:20px;overflow:hidden;background:var(--card-bg);transition:.3s}.project-card:hover{transform:translateY(-7px);border-color:rgba(245,166,35,.55);box-shadow:0 24px 60px rgba(0,0,0,.22)}.project-card.featured{box-shadow:inset 0 0 0 1px rgba(245,166,35,.08)}.mobile-project-card .thumbnail-wrap{background:radial-gradient(circle at 50% 20%,rgba(245,166,35,.12),transparent 35%),#080b10}.mobile-thumbnail-wrap{aspect-ratio:16/10;padding:18px}.mobile-project-thumbnail{width:auto!important;max-width:100%;height:100%!important;margin:auto;padding:0!important;object-fit:contain!important;filter:drop-shadow(0 22px 28px rgba(0,0,0,.48))}.mobile-project-card:hover .mobile-project-thumbnail{transform:translateY(-5px) scale(1.025)}.thumbnail-wrap{position:relative;aspect-ratio:16/10;overflow:hidden;background:#0a0d12;cursor:zoom-in;outline:none}.thumbnail-wrap:focus-visible{box-shadow:inset 0 0 0 3px var(--gold)}.project-thumbnail{width:100%;height:100%;object-fit:contain;object-position:center;display:block;padding:10px;transition:.5s}.project-card:hover .project-thumbnail{transform:scale(1.035)}.thumbnail-overlay{position:absolute;inset:0;display:flex;flex-direction:column;justify-content:flex-end;align-items:flex-start;gap:10px;padding:24px;background:linear-gradient(transparent 35%,rgba(5,7,10,.92));opacity:0;transition:.3s}.project-card:hover .thumbnail-overlay{opacity:1}.thumbnail-overlay span{color:#fff;font-size:12px;letter-spacing:1px;text-transform:uppercase}.thumbnail-overlay a,.thumbnail-overlay button{border:0;background:var(--gold);color:#111;padding:10px 15px;border-radius:8px;font-weight:800;text-decoration:none;cursor:pointer}.view-image-btn{display:inline-flex;align-items:center;justify-content:center}.featured-badge,.project-number{position:absolute;top:18px;border-radius:999px;font-size:11px;font-weight:800}.featured-badge{left:18px;background:var(--gold);color:#111;padding:7px 11px}.project-number{right:18px;background:rgba(13,17,23,.8);color:#fff;border:1px solid rgba(255,255,255,.18);padding:7px 10px}.project-content{padding:26px}.project-topline{display:flex;justify-content:space-between;gap:12px;color:var(--gold);font:700 11px monospace;text-transform:uppercase;letter-spacing:1px}.project-content h3{font-size:28px;line-height:1.2;margin:12px 0}.project-content>p{color:var(--text-muted);margin:0}.project-results{display:flex;flex-wrap:wrap;gap:8px 14px;margin:20px 0;color:var(--text-main);font-size:12px}.project-tags{display:flex;flex-wrap:wrap;gap:8px}.project-tags span{padding:7px 10px;border:1px solid var(--border);border-radius:999px;color:var(--text-muted);font-size:11px;font-weight:700}.project-actions{display:flex;gap:10px;margin-top:24px}.project-primary,.project-secondary{flex:1;text-align:center;padding:11px 14px;border-radius:9px;font-weight:800;text-decoration:none;cursor:pointer}.project-primary{background:var(--gold);color:#111;border:1px solid var(--gold)}.project-secondary{background:transparent;color:var(--text-main);border:1px solid var(--border)}
.center-heading{text-align:center;max-width:760px;margin:0 auto 50px}.center-heading .section-label{justify-content:center}.center-heading p{margin-top:18px}.process-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:18px}.process-grid article{position:relative;padding:27px;border:1px solid var(--border);border-radius:16px;background:var(--card-bg)}.process-number{position:absolute;right:18px;top:15px;color:var(--border);font-size:30px;font-weight:900}.process-icon{display:grid;place-items:center;width:48px;height:48px;border-radius:12px;background:var(--gold-soft);color:var(--gold);font-size:22px}.process-grid h3{margin:20px 0 8px}.process-grid p{color:var(--text-muted);font-size:14px;margin:0}.contact-section{padding-top:30px}.contact-box{text-align:center;padding:72px 28px;border:1px solid var(--border);border-radius:24px;background:radial-gradient(circle at 50% 0,var(--gold-soft),transparent 38%),var(--card-bg)}.availability{display:inline-flex;align-items:center;gap:9px;color:var(--gold);font-size:12px;font-weight:800;text-transform:uppercase;letter-spacing:1px}.availability span{width:8px;height:8px;border-radius:50%;background:var(--gold);box-shadow:0 0 0 6px var(--gold-soft)}.contact-box h2{max-width:800px;margin:22px auto 15px;font-size:clamp(34px,5vw,56px);line-height:1.1}.contact-box p{max-width:700px;margin:auto;color:var(--text-muted)}
.project-modal{position:fixed;inset:0;z-index:9999;display:grid;place-items:center;padding:20px;background:rgba(4,6,9,.82);backdrop-filter:blur(10px)}.modal-card{position:relative;width:min(880px,100%);max-height:92vh;overflow:auto;border:1px solid var(--border);border-radius:20px;background:var(--card-bg);box-shadow:0 30px 90px rgba(0,0,0,.45)}.modal-image-stage{width:100%;aspect-ratio:16/8;display:flex;align-items:center;justify-content:center;overflow:hidden;background:#080b10}.modal-image-stage>img{width:100%;height:100%;object-fit:contain}.mobile-modal-stage{min-height:520px;aspect-ratio:auto;padding:28px;background:radial-gradient(circle at 50% 20%,rgba(245,166,35,.12),transparent 35%),#080b10}.mobile-modal-image{width:auto!important;max-width:100%;height:100%!important;max-height:500px;object-fit:contain!important;filter:drop-shadow(0 25px 35px rgba(0,0,0,.5))}.modal-body{padding:34px}.modal-body h2{font-size:38px;margin:0 0 14px}.modal-body>p{color:var(--text-muted)}.modal-features{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin:24px 0}.modal-features span{padding:12px;background:var(--bg-soft);border:1px solid var(--border);border-radius:9px;font-size:13px}.modal-body .btn-primary{margin-top:24px}.modal-close{position:absolute;right:16px;top:16px;z-index:2;width:40px;height:40px;border:1px solid rgba(255,255,255,.2);border-radius:50%;background:rgba(13,17,23,.8);color:#fff;font-size:25px;cursor:pointer}.image-lightbox{position:fixed;inset:0;z-index:10000;display:flex;align-items:center;justify-content:center;padding:22px;background:rgba(3,5,8,.92);backdrop-filter:blur(12px)}.image-lightbox-card{width:min(1400px,100%);max-height:94vh;display:flex;flex-direction:column;overflow:hidden;border:1px solid var(--border);border-radius:20px;background:var(--card-bg);box-shadow:0 35px 100px rgba(0,0,0,.6)}.image-lightbox-header{display:flex;align-items:center;justify-content:space-between;gap:20px;padding:18px 22px;border-bottom:1px solid var(--border)}.image-lightbox-header span{display:block;color:var(--gold);font:700 10px monospace;letter-spacing:1.2px;text-transform:uppercase}.image-lightbox-header h3{margin:3px 0 0;font-size:20px;line-height:1.2}.image-lightbox-close{flex:0 0 42px;width:42px;height:42px;border:1px solid var(--border);border-radius:50%;background:var(--bg-main);color:var(--text-main);font-size:27px;line-height:1;cursor:pointer}.image-lightbox-close:hover{border-color:var(--gold);color:var(--gold)}.image-lightbox-body{min-height:0;flex:1;display:flex;align-items:center;justify-content:center;overflow:auto;padding:18px;background:#080b10}.image-lightbox-body img{display:block;width:auto;max-width:100%;height:auto;max-height:72vh;object-fit:contain;object-position:center;border-radius:10px}.mobile-lightbox-body{padding:24px;background:radial-gradient(circle at 50% 20%,rgba(245,166,35,.11),transparent 35%),#080b10}.phone-preview-frame{position:relative;width:min(390px,92vw);height:min(78vh,790px);padding:15px 10px 20px;border:3px solid #343b45;border-radius:42px;background:#05070a;box-shadow:0 28px 70px rgba(0,0,0,.65),inset 0 0 0 2px rgba(255,255,255,.035)}.phone-preview-frame img{width:100%!important;height:100%!important;max-height:none!important;object-fit:contain!important;border-radius:30px;background:#0c1118}.phone-speaker{position:absolute;z-index:3;top:8px;left:50%;width:82px;height:6px;transform:translateX(-50%);border-radius:999px;background:#222831}.phone-home-indicator{position:absolute;z-index:3;bottom:7px;left:50%;width:92px;height:4px;transform:translateX(-50%);border-radius:999px;background:#343b45}.image-lightbox-footer{display:flex;justify-content:flex-end;gap:12px;padding:16px 22px;border-top:1px solid var(--border)}.image-lightbox-footer .project-primary,.image-lightbox-footer .project-secondary{flex:0 0 auto;min-width:170px}.project-list-enter-active,.project-list-leave-active{transition:.3s}.project-list-enter-from,.project-list-leave-to{opacity:0;transform:translateY(16px)}.footer{border-top:1px solid var(--border);padding:25px 0;color:var(--text-muted);font-size:13px}.footer-inner{display:flex;justify-content:space-between;gap:15px}
@media(max-width:900px){.section-heading{grid-template-columns:1fr;gap:20px}.projects-grid{grid-template-columns:1fr}.process-grid{grid-template-columns:repeat(2,1fr)}.hero-content h1{letter-spacing:-2px}}@media(max-width:620px){.container{padding:0 16px}.section{padding:78px 0}.projects-hero{padding:130px 0 80px}.hero-content h1{font-size:45px}.hero-content>p{font-size:16px}.hero-stats{grid-template-columns:1fr}.hero-stats article{border-right:0;border-bottom:1px solid var(--border)}.hero-stats article:last-child{border-bottom:0}.process-grid{grid-template-columns:1fr}.project-content{padding:21px}.project-actions{flex-direction:column}.modal-features{grid-template-columns:1fr}.modal-body{padding:24px}.modal-body h2{font-size:30px}.image-lightbox{padding:10px}.image-lightbox-header{padding:14px 15px}.image-lightbox-body{padding:8px}.image-lightbox-body img{max-height:68vh}.phone-preview-frame{width:min(340px,94vw);height:min(72vh,700px);border-radius:36px}.mobile-modal-stage{min-height:420px;padding:18px}.mobile-modal-image{max-height:390px}.image-lightbox-footer{padding:12px;flex-direction:column}.image-lightbox-footer .project-primary,.image-lightbox-footer .project-secondary{width:100%;min-width:0}.footer-inner{flex-direction:column;text-align:center}}
</style>

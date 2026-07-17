<template>
  <div class="contact-page">
    <!-- Agar navbar global component hai to ye line rehne do -->
    <nav-component />

    <!-- HERO SECTION -->
    <section class="contact-hero">
      <div class="hero-grid"></div>

      <span class="hero-glow hero-glow-one"></span>
      <span class="hero-glow hero-glow-two"></span>

      <div class="container hero-content">
        <div class="section-label">Contact Me</div>

        <h1>
          Let’s build something
          <span>professional together.</span>
        </h1>

        <p>
          Tell me about your website, mobile application, business system,
          eCommerce store, Laravel project, or any existing product that needs
          improvement.
        </p>

        <div class="hero-links">
          <a href="mailto:itbilal73@gmail.com">
            <i class="fa-regular fa-envelope"></i>
            itbilal73@gmail.com
          </a>

          <a href="tel:+923015825174">
            <i class="fa-solid fa-phone"></i>
            +92 301 5825174
          </a>

          <a
            href="https://wa.me/923015825174"
            target="_blank"
            rel="noopener noreferrer"
          >
            <i class="fa-brands fa-whatsapp"></i>
            WhatsApp
          </a>
        </div>
      </div>
    </section>

    <!-- CONTACT SECTION -->
    <section class="contact-section">
      <div class="container contact-layout">
        <!-- LEFT SIDE -->
        <aside class="contact-info">
          <div class="section-label">Project Enquiry</div>

          <h2>Share your project requirements.</h2>

          <p class="info-description">
            Complete the form with as much detail as possible. Your message will
            be sent directly to my email, and I will contact you as soon as
            possible.
          </p>

          <div class="info-cards">
            <article>
              <span class="info-icon">
                <i class="fa-regular fa-envelope"></i>
              </span>

              <div>
                <small>Email Address</small>

                <a href="mailto:itbilal73@gmail.com">
                  itbilal73@gmail.com
                </a>
              </div>
            </article>

            <article>
              <span class="info-icon">
                <i class="fa-brands fa-whatsapp"></i>
              </span>

              <div>
                <small>Phone / WhatsApp</small>

                <a
                  href="https://wa.me/923015825174"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                  +92 301 5825174
                </a>
              </div>
            </article>

            <article>
              <span class="info-icon">
                <i class="fa-solid fa-code"></i>
              </span>

              <div>
                <small>Development Services</small>

                <strong>
                  Laravel, Vue.js, Flutter & MySQL
                </strong>
              </div>
            </article>

            <article>
              <span class="info-icon">
                <i class="fa-solid fa-earth-americas"></i>
              </span>

              <div>
                <small>Availability</small>

                <strong>
                  Freelance & Remote Projects
                </strong>
              </div>
            </article>
          </div>

          <div class="response-note">
            <span></span>
            Usually responds within 24 hours
          </div>

          <div class="social-links">
            <a
              href="https://github.com/itbilal78-prosix"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="GitHub"
            >
              <i class="fa-brands fa-github"></i>
            </a>

            <a
              href="https://www.linkedin.com/"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="LinkedIn"
            >
              <i class="fa-brands fa-linkedin-in"></i>
            </a>

            <a
              href="mailto:itbilal73@gmail.com"
              aria-label="Email"
            >
              <i class="fa-regular fa-envelope"></i>
            </a>

            <a
              href="https://wa.me/923015825174"
              target="_blank"
              rel="noopener noreferrer"
              aria-label="WhatsApp"
            >
              <i class="fa-brands fa-whatsapp"></i>
            </a>
          </div>
        </aside>

        <!-- RIGHT SIDE FORM -->
        <div class="form-card">
          <div class="form-heading">
            <span>Start a conversation</span>

            <h2>Tell me about your project</h2>

            <p>
              Fill in the details below and your message will be delivered
              directly to my email inbox.
            </p>
          </div>

          <!-- SUCCESS MESSAGE -->
          <div
            v-if="successMessage"
            class="alert alert-success"
          >
            <span class="alert-icon">
              <i class="fa-solid fa-check"></i>
            </span>

            <div>
              <strong>Message sent successfully</strong>
              <p>{{ successMessage }}</p>
            </div>
          </div>

          <!-- ERROR MESSAGE -->
          <div
            v-if="generalError"
            class="alert alert-error"
          >
            <span class="alert-icon">
              <i class="fa-solid fa-exclamation"></i>
            </span>

            <div>
              <strong>Unable to send message</strong>
              <p>{{ generalError }}</p>
            </div>
          </div>

          <form
            ref="contactForm"
            @submit.prevent="submitForm"
            novalidate
          >
            <!-- HONEYPOT SPAM FIELD -->
            <div class="hidden-field">
              <label for="website">Website</label>

              <input
                id="website"
                v-model="form.website"
                type="text"
                name="website"
                tabindex="-1"
                autocomplete="off"
              />
            </div>

            <div class="form-grid">
              <!-- NAME -->
              <div class="field-group">
                <label for="name">
                  Full Name
                  <span>*</span>
                </label>

                <div class="input-wrapper">
                  <i class="fa-regular fa-user"></i>

                  <input
                    id="name"
                    v-model.trim="form.name"
                    type="text"
                    name="from_name"
                    placeholder="Enter your full name"
                    :class="{ invalid: errors.name }"
                    @input="clearError('name')"
                  />
                </div>

                <span
                  v-if="errors.name"
                  class="field-error"
                >
                  {{ errors.name }}
                </span>
              </div>

              <!-- EMAIL -->
              <div class="field-group">
                <label for="email">
                  Email Address
                  <span>*</span>
                </label>

                <div class="input-wrapper">
                  <i class="fa-regular fa-envelope"></i>

                  <input
                    id="email"
                    v-model.trim="form.email"
                    type="email"
                    name="from_email"
                    placeholder="name@company.com"
                    :class="{ invalid: errors.email }"
                    @input="clearError('email')"
                  />
                </div>

                <span
                  v-if="errors.email"
                  class="field-error"
                >
                  {{ errors.email }}
                </span>
              </div>

              <!-- PHONE -->
              <div class="field-group">
                <label for="phone">
                  Phone / WhatsApp
                </label>

                <div class="input-wrapper">
                  <i class="fa-solid fa-phone"></i>

                  <input
                    id="phone"
                    v-model.trim="form.phone"
                    type="tel"
                    name="phone"
                    inputmode="tel"
                    placeholder="+1 or +92 phone number"
                    :class="{ invalid: errors.phone }"
                    @input="clearError('phone')"
                  />
                </div>

                <span
                  v-if="errors.phone"
                  class="field-error"
                >
                  {{ errors.phone }}
                </span>
              </div>

              <!-- COMPANY -->
              <div class="field-group">
                <label for="company">
                  Company Name
                </label>

                <div class="input-wrapper">
                  <i class="fa-regular fa-building"></i>

                  <input
                    id="company"
                    v-model.trim="form.company"
                    type="text"
                    name="company"
                    placeholder="Your company or brand"
                    :class="{ invalid: errors.company }"
                    @input="clearError('company')"
                  />
                </div>

                <span
                  v-if="errors.company"
                  class="field-error"
                >
                  {{ errors.company }}
                </span>
              </div>

              <!-- SERVICE -->
              <div class="field-group">
                <label for="service">
                  Required Service
                  <span>*</span>
                </label>

                <div class="input-wrapper select-wrapper">
                  <i class="fa-solid fa-layer-group"></i>

                  <select
                    id="service"
                    v-model="form.service"
                    name="service"
                    :class="{ invalid: errors.service }"
                    @change="clearError('service')"
                  >
                    <option
                      value=""
                      disabled
                    >
                      Select a service
                    </option>

                    <option value="Website Development">
                      Website Development
                    </option>

                    <option value="Laravel Web Application">
                      Laravel Web Application
                    </option>

                    <option value="Vue.js Frontend">
                      Vue.js Frontend
                    </option>

                    <option value="Flutter Mobile App">
                      Flutter Mobile App
                    </option>

                    <option value="eCommerce Store">
                      eCommerce Store
                    </option>

                    <option value="CRM / Business System">
                      CRM / Business System
                    </option>

                    <option value="Accounting / Payroll System">
                      Accounting / Payroll System
                    </option>

                    <option value="Bug Fixing / Improvements">
                      Bug Fixing / Improvements
                    </option>

                    <option value="Other">
                      Other
                    </option>
                  </select>
                </div>

                <span
                  v-if="errors.service"
                  class="field-error"
                >
                  {{ errors.service }}
                </span>
              </div>

              <!-- BUDGET -->
              <div class="field-group">
                <label for="budget">
                  Estimated Budget
                </label>

                <div class="input-wrapper select-wrapper">
                  <i class="fa-solid fa-dollar-sign"></i>

                  <select
                    id="budget"
                    v-model="form.budget"
                    name="budget"
                  >
                    <option value="">
                      Select budget range
                    </option>

                    <option value="Under $500">
                      Under $500
                    </option>

                    <option value="$500 - $1,000">
                      $500 - $1,000
                    </option>

                    <option value="$1,000 - $3,000">
                      $1,000 - $3,000
                    </option>

                    <option value="$3,000 - $5,000">
                      $3,000 - $5,000
                    </option>

                    <option value="$5,000+">
                      $5,000+
                    </option>

                    <option value="Need consultation">
                      Need consultation
                    </option>
                  </select>
                </div>
              </div>

              <!-- SUBJECT -->
              <div class="field-group full-width">
                <label for="subject">
                  Project Subject
                  <span>*</span>
                </label>

                <div class="input-wrapper">
                  <i class="fa-regular fa-pen-to-square"></i>

                  <input
                    id="subject"
                    v-model.trim="form.subject"
                    type="text"
                    name="subject"
                    placeholder="Example: Laravel CRM for our company"
                    :class="{ invalid: errors.subject }"
                    @input="clearError('subject')"
                  />
                </div>

                <span
                  v-if="errors.subject"
                  class="field-error"
                >
                  {{ errors.subject }}
                </span>
              </div>

              <!-- MESSAGE -->
              <div class="field-group full-width">
                <div class="label-row">
                  <label for="message">
                    Project Details
                    <span>*</span>
                  </label>

                  <small>
                    {{ form.message.length }}/2000
                  </small>
                </div>

                <div class="textarea-wrapper">
                  <textarea
                    id="message"
                    v-model.trim="form.message"
                    name="message"
                    rows="7"
                    maxlength="2000"
                    placeholder="Describe your project, required features, current website, deadline, and anything important..."
                    :class="{ invalid: errors.message }"
                    @input="clearError('message')"
                  ></textarea>
                </div>

                <span
                  v-if="errors.message"
                  class="field-error"
                >
                  {{ errors.message }}
                </span>
              </div>
            </div>

            <!-- PRIVACY CHECKBOX -->
            <label class="privacy-check">
              <input
                v-model="form.agree"
                type="checkbox"
                name="agree"
                @change="clearError('agree')"
              />

              <span class="custom-checkbox">
                <i class="fa-solid fa-check"></i>
              </span>

              <span class="privacy-text">
                I agree that my information may be used to respond to this
                project enquiry.
              </span>
            </label>

            <span
              v-if="errors.agree"
              class="field-error checkbox-error"
            >
              {{ errors.agree }}
            </span>

            <!-- SUBMIT BUTTON -->
            <button
              class="submit-btn"
              type="submit"
              :disabled="submitting"
            >
              <span
                v-if="submitting"
                class="spinner"
              ></span>

              <i
                v-else
                class="fa-regular fa-paper-plane"
              ></i>

              <span>
                {{
                  submitting
                    ? 'Sending Message...'
                    : 'Send Project Enquiry'
                }}
              </span>

              <i
                v-if="!submitting"
                class="fa-solid fa-arrow-up-right-from-square"
              ></i>
            </button>

            <p class="form-note">
              <i class="fa-solid fa-lock"></i>
              Your information is only used to reply to your enquiry.
            </p>
          </form>
        </div>
      </div>
    </section>

    <!-- SERVICES STRIP -->
    <section class="services-strip">
      <div class="container">
        <div class="service-list">
          <span>Laravel Development</span>
          <i>•</i>

          <span>Vue.js Applications</span>
          <i>•</i>

          <span>Flutter Mobile Apps</span>
          <i>•</i>

          <span>eCommerce</span>
          <i>•</i>

          <span>Business Systems</span>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="container footer-inner">
        <span>
          © {{ currentYear }} Muhammad Bilal — Full-Stack Developer
        </span>

        <span>
          Laravel · Vue.js · Flutter · MySQL
        </span>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { computed, reactive, ref } from 'vue'
import emailjs from '@emailjs/browser'

const contactForm = ref(null)
const submitting = ref(false)
const successMessage = ref('')
const generalError = ref('')

const errors = reactive({
  name: '',
  email: '',
  phone: '',
  company: '',
  service: '',
  subject: '',
  message: '',
  agree: '',
})

const form = reactive({
  name: '',
  email: '',
  phone: '',
  company: '',
  service: '',
  budget: '',
  subject: '',
  message: '',
  agree: false,

  // Spam protection field
  website: '',
})

const currentYear = computed(() => new Date().getFullYear())

const clearErrors = () => {
  Object.keys(errors).forEach((key) => {
    errors[key] = ''
  })
}

const clearError = (field) => {
  if (errors[field]) {
    errors[field] = ''
  }

  successMessage.value = ''
  generalError.value = ''
}

const isValidEmail = (email) => {
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

  return emailPattern.test(email)
}

const isValidPhone = (phone) => {
  if (!phone) {
    return true
  }

  const phonePattern = /^[0-9+\-()\s]{7,25}$/

  return phonePattern.test(phone)
}

const validateForm = () => {
  clearErrors()

  let isValid = true

  if (!form.name || form.name.length < 2) {
    errors.name = 'Please enter your full name.'
    isValid = false
  } else if (form.name.length > 100) {
    errors.name = 'Name must not exceed 100 characters.'
    isValid = false
  }

  if (!form.email) {
    errors.email = 'Please enter your email address.'
    isValid = false
  } else if (!isValidEmail(form.email)) {
    errors.email = 'Please enter a valid email address.'
    isValid = false
  }

  if (!isValidPhone(form.phone)) {
    errors.phone = 'Please enter a valid phone number.'
    isValid = false
  }

  if (form.company && form.company.length > 150) {
    errors.company = 'Company name must not exceed 150 characters.'
    isValid = false
  }

  if (!form.service) {
    errors.service = 'Please select a required service.'
    isValid = false
  }

  if (!form.subject || form.subject.length < 3) {
    errors.subject = 'Please enter your project subject.'
    isValid = false
  } else if (form.subject.length > 180) {
    errors.subject = 'Subject must not exceed 180 characters.'
    isValid = false
  }

  if (!form.message || form.message.length < 20) {
    errors.message =
      'Please provide at least 20 characters about your project.'

    isValid = false
  } else if (form.message.length > 2000) {
    errors.message = 'Message must not exceed 2000 characters.'
    isValid = false
  }

  if (!form.agree) {
    errors.agree = 'Please accept the privacy agreement.'
    isValid = false
  }

  return isValid
}

const resetForm = () => {
  form.name = ''
  form.email = ''
  form.phone = ''
  form.company = ''
  form.service = ''
  form.budget = ''
  form.subject = ''
  form.message = ''
  form.agree = false
  form.website = ''

  clearErrors()
}

const submitForm = async () => {
  successMessage.value = ''
  generalError.value = ''

  // Honeypot spam protection
  if (form.website) {
    successMessage.value =
      'Thank you. Your message has been received.'

    resetForm()
    return
  }

  if (!validateForm()) {
    generalError.value =
      'Please correct the highlighted fields before submitting.'

    const firstInvalidField = document.querySelector(
      '.field-group .invalid'
    )

    if (firstInvalidField) {
      firstInvalidField.scrollIntoView({
        behavior: 'smooth',
        block: 'center',
      })

      firstInvalidField.focus()
    }

    return
  }

  submitting.value = true

  try {
    const serviceId =
      import.meta.env.VITE_EMAILJS_SERVICE_ID

    const templateId =
      import.meta.env.VITE_EMAILJS_TEMPLATE_ID

    const publicKey =
      import.meta.env.VITE_EMAILJS_PUBLIC_KEY

    if (!serviceId || !templateId || !publicKey) {
      throw new Error(
        'EmailJS environment variables are missing.'
      )
    }

    const templateParams = {
      from_name: form.name,
      from_email: form.email,
      phone: form.phone || 'Not provided',
      company: form.company || 'Not provided',
      service: form.service,
      budget: form.budget || 'Not specified',
      subject: form.subject,
      message: form.message,

      // Aapke EmailJS template mein ye variable use ho sakta hai
      reply_to: form.email,

      // EmailJS template ke andar destination email ke liye
      to_name: 'Muhammad Bilal',
      to_email: 'itbilal73@gmail.com',
    }

    await emailjs.send(
      serviceId,
      templateId,
      templateParams,
      {
        publicKey,
      }
    )

    successMessage.value =
      'Thank you! Your project enquiry has been sent. I will contact you as soon as possible.'

    resetForm()

    setTimeout(() => {
      successMessage.value = ''
    }, 10000)
  } catch (error) {
    console.error('EmailJS Error:', error)

    generalError.value =
      'Your message could not be sent. Please try again or contact me directly through email or WhatsApp.'
  } finally {
    submitting.value = false
  }
}
</script>

<style scoped>
:global(:root) {
  --contact-bg-main: #080b10;
  --contact-bg-soft: #0d1117;
  --contact-card-bg: #121820;
  --contact-input-bg: #090d13;
  --contact-text-main: #f4f5f7;
  --contact-text-muted: #99a2b0;
  --contact-border: #28303b;
  --contact-border-soft: rgba(255, 255, 255, 0.07);
  --contact-gold: #f5a623;
  --contact-gold-dark: #d98b0b;
  --contact-gold-soft: rgba(245, 166, 35, 0.12);
  --contact-success: #24c875;
  --contact-danger: #ff5d68;
}

:global(html[data-theme='light']) {
  --contact-bg-main: #f8f7f2;
  --contact-bg-soft: #f1efe8;
  --contact-card-bg: #ffffff;
  --contact-input-bg: #fbfaf7;
  --contact-text-main: #111827;
  --contact-text-muted: #626a76;
  --contact-border: #ddd9cf;
  --contact-border-soft: rgba(17, 24, 39, 0.08);
  --contact-gold: #c88412;
  --contact-gold-dark: #a96e0c;
  --contact-gold-soft: rgba(200, 132, 18, 0.12);
}

* {
  box-sizing: border-box;
}

button,
input,
select,
textarea {
  font-family: inherit;
}

.contact-page {
  min-height: 100vh;
  overflow: hidden;
  background: var(--contact-bg-main);
  color: var(--contact-text-main);
  font-family:
    Inter,
    Montserrat,
    Arial,
    sans-serif;
  line-height: 1.6;
}

.container {
  width: 100%;
  max-width: 1180px;
  margin: 0 auto;
  padding: 0 24px;
}

/* SECTION LABEL */

.section-label {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 16px;
  color: var(--contact-gold);
  font-family: monospace;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.section-label::before {
  content: '';
  width: 32px;
  height: 1px;
  background: var(--contact-gold);
}

/* HERO */

.contact-hero {
  position: relative;
  overflow: hidden;
  padding: 175px 0 110px;
  border-bottom: 1px solid var(--contact-border);
  text-align: center;
}

.hero-grid {
  position: absolute;
  inset: 0;
  background:
    linear-gradient(
      rgba(255, 255, 255, 0.025) 1px,
      transparent 1px
    ),
    linear-gradient(
      90deg,
      rgba(255, 255, 255, 0.025) 1px,
      transparent 1px
    );
  background-size: 54px 54px;
  mask-image: linear-gradient(to bottom, #000, transparent);
  pointer-events: none;
}

.hero-glow {
  position: absolute;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  background: var(--contact-gold);
  filter: blur(130px);
  opacity: 0.11;
  pointer-events: none;
}

.hero-glow-one {
  top: -100px;
  left: 3%;
}

.hero-glow-two {
  right: 3%;
  bottom: -180px;
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 900px;
}

.hero-content h1 {
  max-width: 900px;
  margin: 0 auto;
  font-size: clamp(48px, 7vw, 82px);
  font-weight: 800;
  line-height: 1.02;
  letter-spacing: -4px;
}

.hero-content h1 span {
  display: block;
  color: var(--contact-gold);
}

.hero-content > p {
  max-width: 760px;
  margin: 25px auto 0;
  color: var(--contact-text-muted);
  font-size: 18px;
  line-height: 1.8;
}

.hero-links {
  display: flex;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
  margin-top: 32px;
}

.hero-links a {
  display: inline-flex;
  align-items: center;
  gap: 9px;
  padding: 11px 17px;
  border: 1px solid var(--contact-border);
  border-radius: 999px;
  background: rgba(18, 24, 32, 0.72);
  color: var(--contact-text-main);
  font-size: 13px;
  font-weight: 700;
  text-decoration: none;
  backdrop-filter: blur(12px);
  transition:
    border-color 0.25s ease,
    color 0.25s ease,
    transform 0.25s ease;
}

.hero-links a i {
  color: var(--contact-gold);
}

.hero-links a:hover {
  border-color: var(--contact-gold);
  color: var(--contact-gold);
  transform: translateY(-2px);
}

/* CONTACT SECTION */

.contact-section {
  padding: 105px 0;
  background: var(--contact-bg-soft);
}

.contact-layout {
  display: grid;
  grid-template-columns: 0.8fr 1.2fr;
  gap: 48px;
  align-items: start;
}

/* LEFT INFO */

.contact-info {
  position: sticky;
  top: 110px;
  padding-top: 10px;
}

.contact-info h2 {
  margin: 0;
  font-size: clamp(36px, 5vw, 54px);
  font-weight: 800;
  line-height: 1.1;
  letter-spacing: -2px;
}

.info-description {
  margin: 20px 0 30px;
  color: var(--contact-text-muted);
  font-size: 15px;
  line-height: 1.8;
}

.info-cards {
  display: grid;
  gap: 12px;
}

.info-cards article {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 17px;
  border: 1px solid var(--contact-border);
  border-radius: 14px;
  background: var(--contact-card-bg);
  transition:
    border-color 0.25s ease,
    transform 0.25s ease;
}

.info-cards article:hover {
  border-color: rgba(245, 166, 35, 0.55);
  transform: translateX(4px);
}

.info-icon {
  display: grid;
  place-items: center;
  flex: 0 0 45px;
  width: 45px;
  height: 45px;
  border-radius: 11px;
  background: var(--contact-gold-soft);
  color: var(--contact-gold);
  font-size: 18px;
}

.info-cards small {
  display: block;
  margin-bottom: 2px;
  color: var(--contact-text-muted);
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.info-cards a,
.info-cards strong {
  color: var(--contact-text-main);
  font-size: 14px;
  font-weight: 800;
  text-decoration: none;
}

.info-cards a:hover {
  color: var(--contact-gold);
}

.response-note {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 24px;
  color: var(--contact-text-muted);
  font-size: 13px;
}

.response-note span {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background: var(--contact-success);
  box-shadow: 0 0 0 6px rgba(36, 200, 117, 0.12);
}

.social-links {
  display: flex;
  gap: 10px;
  margin-top: 25px;
}

.social-links a {
  display: grid;
  place-items: center;
  width: 43px;
  height: 43px;
  border: 1px solid var(--contact-border);
  border-radius: 10px;
  background: var(--contact-card-bg);
  color: var(--contact-text-main);
  text-decoration: none;
  transition:
    color 0.25s ease,
    border-color 0.25s ease,
    background 0.25s ease,
    transform 0.25s ease;
}

.social-links a:hover {
  border-color: var(--contact-gold);
  background: var(--contact-gold);
  color: #111111;
  transform: translateY(-3px);
}

/* FORM CARD */

.form-card {
  padding: 36px;
  border: 1px solid var(--contact-border);
  border-radius: 24px;
  background: var(--contact-card-bg);
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.18);
}

.form-heading {
  margin-bottom: 28px;
}

.form-heading > span {
  color: var(--contact-gold);
  font-family: monospace;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
}

.form-heading h2 {
  margin: 7px 0 0;
  font-size: 32px;
  font-weight: 800;
  line-height: 1.2;
}

.form-heading p {
  margin: 9px 0 0;
  color: var(--contact-text-muted);
  font-size: 13px;
}

/* FORM GRID */

.form-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 20px;
}

.full-width {
  grid-column: 1 / -1;
}

.field-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.field-group label {
  color: var(--contact-text-main);
  font-size: 13px;
  font-weight: 800;
}

.field-group label span {
  color: var(--contact-gold);
}

.label-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.label-row small {
  color: var(--contact-text-muted);
  font-size: 11px;
}

/* INPUT */

.input-wrapper {
  position: relative;
}

.input-wrapper > i {
  position: absolute;
  top: 50%;
  left: 15px;
  z-index: 2;
  color: var(--contact-text-muted);
  font-size: 13px;
  transform: translateY(-50%);
  pointer-events: none;
}

.input-wrapper input,
.input-wrapper select,
.textarea-wrapper textarea {
  width: 100%;
  border: 1px solid var(--contact-border);
  outline: none;
  background: var(--contact-input-bg);
  color: var(--contact-text-main);
  font-size: 14px;
  transition:
    border-color 0.2s ease,
    box-shadow 0.2s ease;
}

.input-wrapper input,
.input-wrapper select {
  height: 50px;
  padding: 0 14px 0 43px;
  border-radius: 10px;
}

.input-wrapper select {
  cursor: pointer;
  appearance: none;
  padding-right: 38px;
}

.select-wrapper::after {
  content: '⌄';
  position: absolute;
  top: 46%;
  right: 15px;
  color: var(--contact-text-muted);
  font-size: 17px;
  transform: translateY(-50%);
  pointer-events: none;
}

.textarea-wrapper textarea {
  min-height: 170px;
  padding: 14px;
  border-radius: 10px;
  resize: vertical;
  line-height: 1.7;
}

.input-wrapper input::placeholder,
.textarea-wrapper textarea::placeholder {
  color: #707986;
}

.input-wrapper input:focus,
.input-wrapper select:focus,
.textarea-wrapper textarea:focus {
  border-color: var(--contact-gold);
  box-shadow: 0 0 0 3px var(--contact-gold-soft);
}

.input-wrapper:focus-within > i {
  color: var(--contact-gold);
}

.input-wrapper .invalid,
.textarea-wrapper .invalid {
  border-color: var(--contact-danger);
  box-shadow: 0 0 0 3px rgba(255, 93, 104, 0.08);
}

.field-error {
  color: var(--contact-danger);
  font-size: 11px;
  font-weight: 700;
}

/* CHECKBOX */

.privacy-check {
  position: relative;
  display: flex;
  align-items: flex-start;
  gap: 11px;
  margin-top: 22px;
  color: var(--contact-text-muted);
  font-size: 12px;
  cursor: pointer;
}

.privacy-check input {
  position: absolute;
  opacity: 0;
  pointer-events: none;
}

.custom-checkbox {
  display: grid;
  place-items: center;
  flex: 0 0 18px;
  width: 18px;
  height: 18px;
  margin-top: 2px;
  border: 1px solid var(--contact-border);
  border-radius: 4px;
  background: var(--contact-input-bg);
  color: #111111;
  font-size: 10px;
  transition:
    background 0.2s ease,
    border-color 0.2s ease;
}

.custom-checkbox i {
  opacity: 0;
}

.privacy-check input:checked + .custom-checkbox {
  border-color: var(--contact-gold);
  background: var(--contact-gold);
}

.privacy-check input:checked + .custom-checkbox i {
  opacity: 1;
}

.privacy-text {
  line-height: 1.6;
}

.checkbox-error {
  display: block;
  margin-top: 6px;
}

/* BUTTON */

.submit-btn {
  width: 100%;
  min-height: 54px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-top: 24px;
  border: 1px solid var(--contact-gold);
  border-radius: 11px;
  background: var(--contact-gold);
  color: #111111;
  font-size: 14px;
  font-weight: 900;
  cursor: pointer;
  transition:
    background 0.25s ease,
    box-shadow 0.25s ease,
    transform 0.25s ease;
}

.submit-btn:hover:not(:disabled) {
  background: var(--contact-gold-dark);
  transform: translateY(-2px);
  box-shadow: 0 14px 30px var(--contact-gold-soft);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.spinner {
  width: 18px;
  height: 18px;
  border: 2px solid rgba(0, 0, 0, 0.25);
  border-top-color: #111111;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.form-note {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 7px;
  margin: 12px 0 0;
  color: var(--contact-text-muted);
  text-align: center;
  font-size: 11px;
}

/* ALERTS */

.alert {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  margin-bottom: 22px;
  padding: 15px;
  border-radius: 11px;
}

.alert-icon {
  display: grid;
  place-items: center;
  flex: 0 0 28px;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  font-weight: 900;
}

.alert strong {
  display: block;
  font-size: 13px;
}

.alert p {
  margin: 2px 0 0;
  font-size: 12px;
  line-height: 1.6;
}

.alert-success {
  border: 1px solid rgba(36, 200, 117, 0.35);
  background: rgba(36, 200, 117, 0.09);
  color: #85e9b7;
}

.alert-success .alert-icon {
  background: rgba(36, 200, 117, 0.18);
}

.alert-error {
  border: 1px solid rgba(255, 93, 104, 0.35);
  background: rgba(255, 93, 104, 0.09);
  color: #ff9ca4;
}

.alert-error .alert-icon {
  background: rgba(255, 93, 104, 0.18);
}

/* SPAM FIELD */

.hidden-field {
  position: absolute;
  left: -9999px;
  width: 1px;
  height: 1px;
  overflow: hidden;
  opacity: 0;
}

/* SERVICES STRIP */

.services-strip {
  padding: 28px 0;
  border-top: 1px solid var(--contact-border);
  border-bottom: 1px solid var(--contact-border);
  background: var(--contact-bg-main);
}

.service-list {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 18px;
  flex-wrap: wrap;
  color: var(--contact-text-muted);
  font-family: monospace;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.service-list i {
  color: var(--contact-gold);
  font-style: normal;
}

/* FOOTER */

.footer {
  padding: 25px 0;
  background: var(--contact-bg-main);
  color: var(--contact-text-muted);
  font-size: 13px;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  gap: 15px;
}

/* TABLET */

@media (max-width: 900px) {
  .contact-layout {
    grid-template-columns: 1fr;
  }

  .contact-info {
    position: static;
  }

  .contact-info h2 {
    max-width: 650px;
  }
}

/* MOBILE */

@media (max-width: 620px) {
  .container {
    padding: 0 16px;
  }

  .contact-hero {
    padding: 135px 0 80px;
  }

  .hero-content h1 {
    font-size: 45px;
    letter-spacing: -2px;
  }

  .hero-content > p {
    font-size: 16px;
  }

  .hero-links {
    flex-direction: column;
    align-items: stretch;
  }

  .hero-links a {
    justify-content: center;
  }

  .contact-section {
    padding: 75px 0;
  }

  .form-card {
    padding: 22px 17px;
    border-radius: 18px;
  }

  .form-heading h2 {
    font-size: 27px;
  }

  .form-grid {
    grid-template-columns: 1fr;
  }

  .full-width {
    grid-column: auto;
  }

  .contact-info h2 {
    font-size: 39px;
  }

  .footer-inner {
    flex-direction: column;
    text-align: center;
  }
}

@media (max-width: 420px) {
  .hero-content h1 {
    font-size: 39px;
  }

  .contact-info h2 {
    font-size: 34px;
  }

  .form-card {
    padding: 20px 14px;
  }

  .info-cards article {
    padding: 14px;
  }

  .info-cards a,
  .info-cards strong {
    font-size: 13px;
  }
}
</style>

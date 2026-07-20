<template>
  <div class="min-h-screen font-sans text-gray-800 overflow-x-hidden " id="top">
    <Header @open-login="showLogin = true" @open-register="showRegister = true" />

 <HeroSection />

    <BgSection />

    <HowItWorksSection />

    <WhoCanJoinSection />
    <FaqSection />

   
   <CtaSection />

    <Footer />

    <!-- Scroll to top -->
    <transition
      enter-active-class="transition-all duration-300 ease-out" enter-from-class="opacity-0 translate-y-4" enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"  leave-from-class="opacity-100 translate-y-0" leave-to-class="opacity-0 translate-y-4">
      <button v-if="showScrollTop" @click="scrollToTop"
        class="fixed bottom-8 right-8 z-50 w-12 h-12 bg-primary hover:bg-primary-dark text-white
               rounded-2xl shadow-xl shadow-primary/35 flex items-center justify-center
               hover:-translate-y-1 transition-all duration-300">
        <i class="fas fa-arrow-up text-sm"></i>
      </button>
    </transition>

    <login-modal    v-if="showLogin"    @close="showLogin = false"    @switch-to-register="showLogin = false; showRegister = true" />
    <register-modal v-if="showRegister" @close="showRegister = false" @switch-to-login="showRegister = false; showLogin = true" />
  </div>
</template>

<script>
import Header        from './header.vue';
import Footer        from './footer.vue';
import LoginModal    from '@/components/AuthModal.vue';
import RegisterModal from '@/components/RegisterModal.vue';


import BgSection from "./sections/BgSection.vue"
import FaqSection from "./sections/FaqSection.vue"
import HeroSection from "./sections/HeroSection.vue"
import CtaSection from "./sections/CtaSection.vue"
import HowItWorksSection from "./sections/HowItWorksSection.vue"
import WhoCanJoinSection from "./sections/WhoCanJoinSection.vue"

export default {
  name: 'HomePage',
  components: { Header, Footer, LoginModal, RegisterModal,BgSection,FaqSection,HeroSection,FaqSection,CtaSection,HowItWorksSection ,WhoCanJoinSection},

  data() {
    return {
      showLogin:      false,
      showRegister:   false,
      contactLoading: false,
      contactSuccess: false,
      contactForm:    { org_name: '', email: '', message: '' },
      showScrollTop:  false,
      openFaq:        null,

      aboutCards: [
        { title: 'Know Your Members',  desc: 'Every profile searchable by skill, profession, and location.',       icon: 'fas fa-id-badge',     bg: 'bg-primary-lighter',   color: 'text-primary' },
        { title: 'Fast Mobilization',  desc: 'Coordinators find the right people in minutes, not days.',           icon: 'fas fa-bolt',         bg: 'bg-secondary-lighter', color: 'text-secondary' },
        { title: 'Skills-Based Match', desc: 'Tasks matched to members based on real expertise and availability.', icon: 'fas fa-puzzle-piece', bg: 'bg-tertiary-lighter',  color: 'text-tertiary' },
        { title: 'Privacy First',      desc: 'Encrypted data, shared only with authorized coordinators.',          icon: 'fas fa-shield-alt',   bg: 'bg-primary-lighter',   color: 'text-primary' },
      ],

      steps: [
        { title: 'Create Your Profile',      desc: 'Register your name, profession, skills, location, and availability in just a few minutes.',            icon: 'fas fa-user-plus' },
        { title: 'Get Verified & Connected', desc: 'A coordinator reviews and activates your profile so you appear in search and matching results.',       icon: 'fas fa-user-check' },
        { title: 'Contribute & Grow',        desc: 'Get matched to campaigns, tasks, and opportunities that fit your unique skills and availability.',     icon: 'fas fa-hands-helping' },
      ],

      audiences: [
        { title: 'Professionals',     desc: 'Lawyers, doctors, engineers, teachers, and researchers contributing their expertise to the cause.',  icon: 'fas fa-briefcase' },
        { title: 'Students & Youth',  desc: 'University students and graduates eager to make a meaningful impact in their region.',                icon: 'fas fa-user-graduate' },
        { title: 'Communicators',     desc: 'Journalists, advocates, and content creators amplifying the voice of the peaceful movement.',        icon: 'fas fa-bullhorn' },
        { title: 'Community Leaders', desc: 'Local organizers and representatives bridging the movement to every corner of Tigray.',              icon: 'fas fa-people-carry' },
      ],

      faqs: [
        { q: 'Who can register on this platform?',
          a: 'Any member of the CPCT Youth Wing of the Peaceful Struggle Movement can register. If you are a young person who supports justice and peace in Tigray, you are welcome.' },
        { q: 'Is my personal data safe?',
          a: 'Yes. All data is encrypted and protected by role-based access controls. Your information is only visible to verified coordinators and never shared externally without your consent.' },
        { q: 'Do I need technical experience to use it?',
          a: 'Not at all. The platform is designed to be simple and intuitive, even for members with no technical background. A Tigrinya interface is also available.' },
        { q: 'How will I be contacted after registering?',
          a: 'Once your profile is activated, you may be reached through the platform when there is an opportunity that matches your skills or availability.' },
        { q: 'Can I update my profile after registering?',
          a: 'Yes. You can log in at any time to update your skills, location, availability, or any other information.' },
        { q: 'Is there a cost to join?',
          a: 'No. Registration and use of the CPCT-Youth platform is completely free for all members.' },
      ],

      contactInfo: [
        { label: 'Location', value: 'Addis Ababa, Ethiopia',          icon: 'fas fa-map-marker-alt' },
        { label: 'Email',    value: 'cpct.youth@peacefulstruggle.et', icon: 'fas fa-envelope' },
        { label: 'Telegram', value: '@CPCTYouth',                     icon: 'fab fa-telegram-plane' },
      ],
    };
  },

  methods: {
    toggleFaq(i) { this.openFaq = this.openFaq === i ? null : i; },
    scrollToTop() { window.scrollTo({ top: 0, behavior: 'smooth' }); },
    async submitContact() {
      this.contactLoading = true;
      this.contactSuccess = false;
      try { await this.$apiPost('/contact', this.contactForm); } catch { /* best-effort */ }
      this.contactSuccess = true;
      this.contactForm    = { org_name: '', email: '', message: '' };
      this.contactLoading = false;
    },
    initReveal() {
      const obs = new IntersectionObserver((entries) => {
        entries.forEach(e => {
          if (e.isIntersecting) { e.target.classList.add('revealed'); obs.unobserve(e.target); }
        });
      }, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });
      document.querySelectorAll('.reveal-up, .reveal-left, .reveal-right').forEach(el => obs.observe(el));
    },
    handleScroll() { this.showScrollTop = window.scrollY > 400; },
  },

  mounted() {
    this.$nextTick(() => {
      document.querySelectorAll('.hero-text').forEach(el => {
        setTimeout(() => el.classList.add('revealed'), 80);
      });
      this.initReveal();
    });
    window.addEventListener('scroll', this.handleScroll, { passive: true });
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  },
};
</script>

<style scoped>
/* ── Reveal animations ── */
.reveal-up, .reveal-left, .reveal-right, .hero-text {
  opacity: 0;
  transition: opacity 0.85s cubic-bezier(0.16, 1, 0.3, 1),
              transform 0.85s cubic-bezier(0.16, 1, 0.3, 1);
}
.reveal-up    { transform: translateY(40px); }
.reveal-left  { transform: translateX(-50px); }
.reveal-right { transform: translateX(50px); }
.hero-text    { transform: translateY(24px); }

.reveal-up.revealed,
.reveal-left.revealed,
.reveal-right.revealed,
.hero-text.revealed { opacity: 1; transform: translate(0, 0); }

.reveal-up:nth-child(2) { transition-delay: 0.10s; }
.reveal-up:nth-child(3) { transition-delay: 0.20s; }
.reveal-up:nth-child(4) { transition-delay: 0.30s; }
.reveal-up:nth-child(5) { transition-delay: 0.40s; }

/* ── Floating dove ── */
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50%       { transform: translateY(-5px); }
}
.animate-float { animation: float 3s ease-in-out infinite; }
</style>

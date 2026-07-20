<template>
  <div class="min-h-screen bg-white font-sans text-gray-800 ">
    <Header @open-login="showLogin = true" @open-register="showRegister = true" />

    <!-- ══════════════════════════════════════════════════════════
         HERO
    ══════════════════════════════════════════════════════════ -->
    <section class="relative bg-slate-900 py-24 overflow-hidden">
      <div class="absolute inset-0 opacity-[0.12] pointer-events-none">
        <div class="absolute top-0 right-0 w-96 h-96 bg-primary rounded-full blur-3xl"></div>
        <div class="absolute bottom-0 left-0 w-72 h-72 bg-secondary rounded-full blur-3xl"></div>
      </div>
      <div class="absolute inset-0 opacity-[0.04] pointer-events-none"
        style="background-image:radial-gradient(circle,#fff 1px,transparent 1px);background-size:32px 32px">
      </div>
      <div class="relative max-w-4xl mx-auto px-6 text-center">
        <span class="inline-block px-4 py-1.5 mb-6 text-xs font-semibold tracking-widest
                     text-primary-light bg-primary/10 rounded-full uppercase border border-primary/20">
          <i class="fas fa-dove mr-2"></i>About CPCT-Youth
        </span>
        <h1 class="text-4xl sm:text-5xl font-black text-white leading-tight mb-6">
          The Movement Behind<br/>
          <span class="text-primary-light">Youth-Led Peaceful Change</span>
        </h1>
        <p class="text-slate-400 text-lg leading-relaxed max-w-2xl mx-auto">
          The CPCT Youth Wing is the organized force of young professionals, students, and community
          leaders committed to advancing justice, peace, and democratic values in Tigray through
          non-violent, coordinated action.
        </p>
      </div>
    </section>

    <!-- ══════════════════════════════════════════════════════════
         MISSION  (white bg)
    ══════════════════════════════════════════════════════════ -->
    <section class="py-20 bg-white relative overflow-hidden">
      <div class="absolute top-0 right-0 w-[400px] h-[400px] bg-primary/5 rounded-full blur-[90px] pointer-events-none"></div>
      <div class="max-w-6xl mx-auto px-6 grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
        <div>
          <span class="text-xs font-bold tracking-[0.2em] text-primary uppercase">Our Mission</span>
          <h2 class="text-3xl font-black text-gray-900 mt-3 mb-6 leading-tight">
            Uniting youth talent for a peaceful and just Tigray
          </h2>
          <p class="text-gray-500 leading-relaxed mb-4 text-sm">
            The Coordinating Platform of Change for Tigray (CPCT) Youth Wing exists to organize the collective
            intelligence, skills, and energy of young Tigrayans into a structured, peaceful force for positive change.
          </p>
          <p class="text-gray-500 leading-relaxed mb-4 text-sm">
            We believe that lasting peace is built through systematic, non-violent engagement — and that the youth
            of Tigray carry the expertise, passion, and commitment needed to lead this process.
          </p>
          <p class="text-gray-500 leading-relaxed text-sm">
            This digital platform is our tool to <strong class="text-gray-700">know our members</strong>,
            <strong class="text-gray-700">connect their skills to action</strong>, and
            <strong class="text-gray-700">coordinate effectively</strong> across professions, regions, and roles.
          </p>
        </div>
      
      </div>
    </section>

    <!-- ══════════════════════════════════════════════════════════
         WHAT WE STAND FOR  (green-50 bg)
    ══════════════════════════════════════════════════════════ -->
    <section class="py-20 bg-green-50 relative overflow-hidden">
      <div class="absolute top-0 left-1/2 -translate-x-1/2 w-[500px] h-[200px]
                  bg-primary/5 rounded-full blur-[70px] pointer-events-none"></div>
      <div class="max-w-6xl mx-auto px-6">
        <div class="text-center mb-14">
          <span class="text-xs font-bold tracking-[0.2em] text-primary uppercase">Core Principles</span>
          <h2 class="text-3xl font-black text-gray-900 mt-3">What guides us</h2>
          <p class="text-gray-500 mt-3 max-w-2xl mx-auto text-sm leading-relaxed">
            The CPCT Youth Wing operates on three unshakeable foundations that shape every action and decision.
          </p>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div v-for="principle in principles" :key="principle.title"
            class="group bg-white border border-green-100 rounded-2xl p-7
                   hover:border-primary/30 hover:shadow-xl hover:shadow-primary/6
                   hover:-translate-y-1 transition-all duration-300">
            <div class="w-12 h-12 rounded-xl bg-primary-lighter flex items-center justify-center mb-5
                        group-hover:scale-110 transition-transform duration-300">
              <i :class="[principle.icon, 'text-primary text-lg']"></i>
            </div>
            <h3 class="font-black text-gray-800 mb-3 text-base group-hover:text-primary transition-colors duration-300">
              {{ principle.title }}
            </h3>
            <p class="text-sm text-gray-500 leading-relaxed">{{ principle.desc }}</p>
          </div>
        </div>
      </div>
    </section>

   
  
    <section class="py-20 bg-green-50">
      <div class="max-w-6xl mx-auto px-6">
        <div class="text-center mb-14">
          <span class="text-xs font-bold tracking-[0.2em] text-primary uppercase">Who We Serve</span>
          <h2 class="text-3xl font-black text-gray-900 mt-3">Built for every young Tigrayan</h2>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-5">
          <div v-for="uc in whoWeServe" :key="uc.title"
            class="group bg-white border border-green-100 rounded-2xl p-6 text-center
                   hover:border-primary/30 hover:shadow-md hover:-translate-y-1 transition-all duration-300">
            <div class="w-12 h-12 rounded-2xl bg-primary-lighter flex items-center justify-center
                        mx-auto mb-4 group-hover:scale-110 transition-transform duration-300">
              <i :class="[uc.icon, 'text-primary text-lg']"></i>
            </div>
            <h3 class="font-black text-gray-800 mb-2 text-sm group-hover:text-primary transition-colors duration-300">{{ uc.title }}</h3>
            <p class="text-xs text-gray-500 leading-relaxed">{{ uc.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ══════════════════════════════════════════════════════════
         VALUES  (slate-900 dark bg — kept for visual weight)
    ══════════════════════════════════════════════════════════ -->
    <section class="py-20 bg-slate-900 relative overflow-hidden">
      <div class="absolute inset-0 opacity-[0.08] pointer-events-none">
        <div class="absolute top-0 right-0 w-96 h-96 bg-primary rounded-full blur-3xl"></div>
        <div class="absolute bottom-0 left-0 w-72 h-72 bg-secondary rounded-full blur-3xl"></div>
      </div>
      <div class="relative max-w-6xl mx-auto px-6">
        <div class="text-center mb-14">
          <span class="text-xs font-bold tracking-[0.2em] text-primary-light uppercase">Our Values</span>
          <h2 class="text-3xl font-black text-white mt-3">What we stand for</h2>
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-5">
          <div v-for="val in values" :key="val.title"
            class="bg-white/5 border border-white/10 rounded-2xl p-6
                   hover:bg-white/10 hover:border-primary/30 transition-all duration-300">
            <i :class="[val.icon, 'text-primary-light text-xl mb-4 block']"></i>
            <h3 class="font-bold text-white mb-2">{{ val.title }}</h3>
            <p class="text-sm text-white/50 leading-relaxed">{{ val.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ══════════════════════════════════════════════════════════
         CTA  (green-50 bg)
    ══════════════════════════════════════════════════════════ -->
    <section class="py-20 bg-green-50 relative overflow-hidden">
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2
                  w-[500px] h-[250px] bg-primary/7 rounded-full blur-[80px] pointer-events-none"></div>
      <div class="relative max-w-3xl mx-auto px-6 text-center">
        <h2 class="text-3xl font-black text-gray-900 mb-4">Ready to join the movement?</h2>
        <p class="text-gray-500 mb-8 text-sm leading-relaxed">
          Register your profile today. Your skills, profession, and commitment are exactly what the peaceful struggle needs.
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <button @click="showRegister = true"
            class="px-8 py-4 bg-primary hover:bg-primary-dark text-white font-bold rounded-xl
                   shadow-lg shadow-primary/20 hover:-translate-y-0.5 transition-all duration-300 text-sm">
            Register Your Profile — Free
          </button>
          <router-link to="/contact"
            class="px-8 py-4 bg-white border border-green-200 hover:border-primary/40 text-gray-700
                   hover:text-primary font-semibold rounded-xl transition-all duration-300 text-sm shadow-sm">
            Contact the Committee
          </router-link>
        </div>
      </div>
    </section>

    <Footer />

    <login-modal    v-if="showLogin"    @close="showLogin = false"    @switch-to-register="showLogin = false; showRegister = true" />
    <register-modal v-if="showRegister" @close="showRegister = false" @switch-to-login="showRegister = false; showLogin = true" />
  </div>
</template>

<script>
import Header        from './header.vue';
import Footer        from './footer.vue';
import LoginModal    from '@/components/AuthModal.vue';
import RegisterModal from '@/components/RegisterModal.vue';

export default {
  name: 'AboutPage',
  components: { Header, Footer, LoginModal, RegisterModal },

  data() {
    return {
      showLogin: false,
      showRegister: false,

      missionStats: [
        { value: '5,000+', label: 'Youth Capacity' },
        { value: '20+',    label: 'Skill Categories' },
        { value: '3',      label: 'Access Roles' },
        { value: '100%',   label: 'Non-violent Approach' },
      ],

      principles: [
        {
          title: 'Non-Violence',
          desc:  'Every action, campaign, and mobilization is grounded in peaceful, non-violent methods. We believe change achieved through dignity lasts longer.',
          icon:  'fas fa-dove',
        },
        {
          title: 'Collective Strength',
          desc:  'Individual talent becomes transformative only when organized. The platform turns scattered expertise into coordinated collective power.',
          icon:  'fas fa-people-arrows',
        },
        {
          title: 'Justice & Accountability',
          desc:  'We work toward a Tigray where rights are respected, institutions are accountable, and all citizens live with dignity.',
          icon:  'fas fa-balance-scale',
        },
      ],

      strategySteps: [
        { phase: 'Step 1', title: 'Assessment',        icon: 'fas fa-search',           desc: 'We begin by understanding the current state — who our members are, what skills they hold, and where gaps exist.' },
        { phase: 'Step 2', title: 'Gap Analysis',      icon: 'fas fa-chart-line',        desc: 'We identify where the movement is today, where we need to go, and what expertise is required to get there.' },
        { phase: 'Step 3', title: 'Strategic Planning', icon: 'fas fa-lightbulb',        desc: 'We co-develop targeted action plans with the coordinating committee — matching skills to specific campaigns and tasks.' },
        { phase: 'Step 4', title: 'Execution',         icon: 'fas fa-hands-helping',     desc: 'We mobilize the right members, implement coordinated actions, and track progress toward peaceful outcomes.' },
      ],

      whoWeServe: [
        { title: 'Professionals',      desc: 'Lawyers, doctors, engineers, and educators contributing specialized expertise.',      icon: 'fas fa-briefcase' },
        { title: 'Students & Youth',   desc: 'Young graduates bringing fresh energy, digital skills, and grassroots connections.',  icon: 'fas fa-user-graduate' },
        { title: 'Communicators',      desc: 'Journalists, writers, and social media advocates amplifying the peaceful message.',   icon: 'fas fa-bullhorn' },
        { title: 'Community Leaders',  desc: 'Local organizers bridging the movement to every corner of Tigray.',                  icon: 'fas fa-people-carry' },
      ],

      values: [
        { title: 'Non-Violence',        desc: 'Every method and action must remain within the bounds of peaceful, dignified resistance.',        icon: 'fas fa-dove' },
        { title: 'Inclusion',           desc: 'Every young Tigrayan — regardless of gender, profession, or location — has a place in the movement.', icon: 'fas fa-users' },
        { title: 'Data Privacy',        desc: 'Member information is encrypted, consent-managed, and never shared without authorization.',        icon: 'fas fa-lock' },
        { title: 'Accountability',      desc: 'Leadership and coordinators are held to high standards of transparency and service.',              icon: 'fas fa-balance-scale' },
        { title: 'Skills-Based Action', desc: 'We match the right expertise to the right task — maximizing the impact of every member.',         icon: 'fas fa-puzzle-piece' },
        { title: 'Continuous Growth',   desc: 'The platform and the movement evolve together, learning from each campaign and coordination.',    icon: 'fas fa-sync-alt' },
      ],
    };
  },
};
</script>

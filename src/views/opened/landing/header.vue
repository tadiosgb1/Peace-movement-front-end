<template>
  <header class="fixed top-0 left-0 right-0 z-[100] shadow-md">

   
   

    <!-- ── Main Nav Bar ── -->
    <div class="bg-white border-b border-brand-border">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3 flex items-center justify-between">

        <!-- Logo -->
        <router-link to="/" class="flex items-center gap-3 group">
          <div class="relative">
            <div class="absolute inset-0 rounded-full bg-primary-light blur-md opacity-30 group-hover:opacity-60 transition-opacity duration-300"></div>
            <div class="absolute inset-[-3px] rounded-full border-2 border-dashed border-primary/40 group-hover:border-primary-light animate-spin-slow transition-colors duration-300"></div>
            <div class="relative w-11 h-11 rounded-full bg-gradient-to-br from-primary to-tertiary-light flex items-center justify-center ring-2 ring-white shadow-lg group-hover:scale-105 transition-transform duration-300">
              <i class="fas fa-dove text-white text-lg"></i>
            </div>
          </div>
          <div class="flex flex-col leading-none">
            <span class="text-base font-black text-gray-900 tracking-tight">
              CPCT<span class="text-primary-light">-Youth</span>
            </span>
            <span class="text-[9px] font-medium text-brand-muted uppercase tracking-widest mt-0.5 hidden sm:block">
              Peaceful Struggle Movement
            </span>
          </div>
        </router-link>

        <!-- Desktop Nav -->
        <nav class="hidden lg:flex items-center gap-1">
          <router-link
            v-for="nav in navLinks"
            :key="nav.path"
            :to="nav.path"
            class="px-4 py-2 text-gray-600 text-xs font-semibold uppercase tracking-wider hover:text-primary-light hover:bg-primary-lighter rounded-lg transition-all"
            active-class="text-primary bg-primary-lighter"
          >
            {{ nav.name }}
          </router-link>
        </nav>

        <!-- Desktop Actions -->
        <div class="hidden md:flex items-center gap-3">
          <button
            @click="$emit('open-login')"
            class="px-5 py-2 text-gray-600 hover:text-primary text-xs font-semibold uppercase tracking-wider rounded-lg hover:bg-primary-lighter transition border border-gray-200 hover:border-brand-border"
          >
            Sign In
          </button>
          <button
            @click="$emit('open-register')"
            class="px-5 py-2 bg-primary hover:bg-primary-dark text-white text-xs font-semibold uppercase tracking-wider rounded-xl shadow shadow-primary/30 transition"
          >
            Join Now
          </button>
        </div>

        <!-- Mobile menu button -->
        <button
          @click="mobileMenuOpen = !mobileMenuOpen"
          class="lg:hidden w-9 h-9 flex items-center justify-center rounded-xl bg-gray-100 text-gray-600 hover:bg-primary-lighter hover:text-primary transition"
          :class="{ 'bg-primary-lighter text-primary': mobileMenuOpen }"
        >
          <i class="fas text-sm" :class="mobileMenuOpen ? 'fa-times' : 'fa-bars'"></i>
        </button>
      </div>

      <!-- Mobile Menu -->
      <transition
        enter-active-class="transition duration-200 ease-out"
        enter-from-class="opacity-0 -translate-y-2"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition duration-150 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-2"
      >
        <div v-if="mobileMenuOpen" class="lg:hidden bg-white border-t border-gray-100 px-4 pb-4 pt-2 space-y-1">
          <router-link
            v-for="nav in navLinks"
            :key="nav.path"
            :to="nav.path"
            @click="mobileMenuOpen = false"
            class="flex items-center justify-between px-4 py-3 rounded-xl text-gray-600 hover:text-primary hover:bg-primary-lighter text-sm font-semibold transition"
          >
            {{ nav.name }}
            <i class="fas fa-chevron-right text-[10px] text-gray-300"></i>
          </router-link>

          <div class="pt-2 pb-1 px-4 flex flex-col gap-1 text-xs text-gray-500">
            <a href="tel:+251914000000" class="flex items-center gap-2 hover:text-primary transition">
              <i class="fas fa-phone-alt text-primary-light"></i> +251 914 000 000
            </a>
            <a href="mailto:cpct.youth@peacefulstruggle.et" class="flex items-center gap-2 hover:text-primary transition">
              <i class="fas fa-envelope text-primary-light"></i> cpct.youth@peacefulstruggle.et
            </a>
          </div>

          <div class="pt-3 border-t border-gray-100 flex flex-col gap-2">
            <button
              @click="mobileMenuOpen = false; $emit('open-login')"
              class="w-full py-3 text-gray-600 hover:text-primary text-sm font-semibold rounded-xl hover:bg-primary-lighter transition border border-gray-200"
            >
              Sign In
            </button>
            <button
              @click="mobileMenuOpen = false; $emit('open-register')"
              class="w-full py-3 bg-primary hover:bg-primary-dark text-white text-sm font-semibold rounded-xl transition"
            >
              Join the Movement
            </button>
          </div>
        </div>
      </transition>
    </div>

  </header>
</template>

<script>
export default {
  name: 'SiteHeader',
  emits: ['open-login', 'open-register'],

  data() {
    return {
      mobileMenuOpen: false,
      navLinks: [
        { name: 'Home',        path: '/' },
        { name: 'About',       path: '/about' },
        { name: 'News',        path: '/news-events' },
        { name: 'Contact',     path: '/contact' },
      ],
    };
  },

  watch: {
    $route() {
      this.mobileMenuOpen = false;
    },
  },
};
</script>

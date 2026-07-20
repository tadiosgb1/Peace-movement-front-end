<template>
  <div class="min-h-screen bg-white font-sans text-gray-800 ">
    <Header @open-login="showLogin = true" @open-register="showRegister = true" />

    <!-- ══════════════════════════════════════════════════════════
         CONTACT SECTION
         ══════════════════════════════════════════════════════════ -->
    <section id="contact" class="py-32 bg-white relative overflow-hidden">
      <div class="absolute top-0 left-0 w-full h-full opacity-[0.02] pointer-events-none -z-0" 
           style="background-image: linear-gradient(#3d5afe 1px, transparent 1px), linear-gradient(90deg, #3d5afe 1px, transparent 1px); background-size: 50px 50px;">
      </div>
      
      <div class="max-w-7xl mx-auto px-6 relative z-10">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 items-start">
          
          <!-- Left Info Panel -->
          <div class="lg:col-span-5 space-y-8">
            <div>
              <span class="inline-block px-4 py-1.5 mb-6 text-[10px] font-black tracking-[0.3em] text-primary bg-primary/10 rounded-full uppercase">
                Get Involved
              </span>
              <h2 class="text-6xl font-black text-slate-900 mb-8 tracking-tighter leading-[0.9]">
                Coordinate Your <br/> <span class="text-primary">Impact.</span>
              </h2>
              <p class="text-slate-500 text-lg font-medium leading-relaxed max-w-md">
                Have questions about the movement, regional committees, or how your specialized professional skills can support peaceful change? Reach out directly.
              </p>
            </div>

            <div class="grid grid-cols-1 gap-4">
              <div v-for="info in contactInfo" :key="info.label" 
                   class="group p-6 bg-slate-50 border border-slate-100 rounded-[2rem] hover:bg-primary hover:border-primary transition-all duration-500 flex items-center gap-6">
                <div class="w-14 h-14 rounded-2xl bg-white shadow-sm flex items-center justify-center text-primary group-hover:scale-110 transition-transform">
                  <i :class="info.icon" class="text-xl"></i>
                </div>
                <div>
                  <p class="text-[10px] font-black uppercase tracking-widest text-slate-400 group-hover:text-white/60 mb-1">{{ info.label }}</p>
                  <p class="text-md font-bold text-slate-800 group-hover:text-white">{{ info.value }}</p>
                </div>
              </div>
            </div>

          
          </div>

          <!-- Right Form Panel -->
          <div class="lg:col-span-7">
            <div class="bg-white rounded-[3rem] p-10 md:p-16 shadow-[0_32px_64px_-16px_rgba(0,0,0,0.08)] border border-slate-100 relative">
              <div class="absolute -top-6 -right-6 w-24 h-24 bg-secondary rounded-3xl -rotate-12 -z-10 opacity-20"></div>
              
              <form @submit.prevent="submitForm" class="space-y-10">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
                  <div class="space-y-2">
                    <label class="text-[11px] font-black uppercase tracking-widest text-slate-500 ml-1">Full Name </label>
                    <input type="text" v-model="form.name" required placeholder="" 
                      class="w-full bg-slate-100/70 border border-primary focus:border-secondary rounded-md px-6 py-4 outline-none focus:ring-2 focus:ring-primary/20 transition-all font-bold text-slate-900 placeholder:text-slate-400" />
                  </div>
                  <div class="space-y-2">
                    <label class="text-[11px] font-black uppercase tracking-widest text-slate-500 ml-1">Contact Email</label>
                    <input type="email" v-model="form.email" required placeholder="" 
                      class="w-full bg-slate-100/70 border border-primary focus:border-secondary rounded-md px-6 py-4 outline-none focus:ring-2 focus:ring-primary/20 transition-all font-bold text-slate-900 placeholder:text-slate-400" />
                  </div>

                </div>

                <div class="space-y-2">
                  <label class="text-[11px] font-black uppercase tracking-widest text-slate-500 ml-1">Message</label>
                  <textarea v-model="form.message" rows="4" placeholder="" 
                    class="w-full bg-slate-100/70 border border-primary focus:border-secondary rounded-md px-6 py-4 outline-none focus:ring-2 focus:ring-primary/20 transition-all font-bold text-slate-900 resize-none placeholder:text-slate-400"></textarea>
                </div>

                <button
                  type="submit"
                  :disabled="loading"
                  class="w-full bg-primary hover:bg-slate-900 text-white py-6 rounded-[2rem] font-black text-xs uppercase tracking-[0.4em] transition-all duration-500 shadow-2xl shadow-primary/30 flex items-center justify-center gap-4 group"
                >
                  {{ loading ? 'Sending Message...' : 'Send Message' }}
                  <i class="fas fa-arrow-right group-hover:translate-x-2 transition-transform"></i>
                </button>
              </form>
            </div>
          </div>

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
  name: 'ContactPage',
  components: { Header, Footer, LoginModal, RegisterModal },

  data() {
    return {
      showLogin: false,
      showRegister: false,
      loading: false,
      contactInfo: [
        { label: 'Coordination HQ', value: 'Mekelle, Tigray, Ethiopia', icon: 'fas fa-map-marker-alt' },
        { label: 'Committee Support', value: 'info@cpct-youth.org', icon: 'fas fa-envelope' },
        { label: 'Hotline / Signal', value: '+251 911 00 11 22', icon: 'fas fa-phone-alt' },
      ],
      form: {
        name: "",
        email: "",
        message: "",
      },
    };
  },
  methods: {
    async submitForm() {
      this.loading = true;
      setTimeout(() => {
        alert("Message sent successfully. The CPCT Youth Wing coordinating committee will reply within 24 hours.");
        this.loading = false;
        this.form = { name: "", email: "", message: "" };
      }, 1500);
    }
  }
};
</script>

<style scoped>
input, textarea {
  box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.02);
}
</style>
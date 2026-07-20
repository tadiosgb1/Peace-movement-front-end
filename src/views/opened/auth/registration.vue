<template>
  <div class="fixed inset-0 z-[200] flex items-center justify-center p-4">
    <!-- Backdrop -->
    <div class="absolute inset-0 bg-slate-900/70 backdrop-blur-sm" @click="$emit('close')"></div>

    <!-- Modal -->
    <div class="relative w-full max-w-xl md:max-w-4xl bg-white shadow-2xl rounded-3xl overflow-hidden max-h-[90vh] flex flex-col transition-all duration-300">

      <!-- Top accent bar -->
      <div class="h-1.5 w-full bg-gradient-to-r from-primary to-primary-light flex-shrink-0"></div>

      <!-- Close -->
      <button @click="$emit('close')"
        class="absolute top-5 right-5 w-8 h-8 flex items-center justify-center
               rounded-full bg-slate-100 hover:bg-slate-200 text-slate-500 transition z-10">
        <i class="fas fa-times text-xs"></i>
      </button>

      <!-- Scrollable body -->
      <div class="overflow-y-auto flex-1 p-6 md:p-10">

        <!-- Header -->
        <div class="flex items-center gap-3 mb-2">
          <div class="w-9 h-9 bg-primary rounded-xl flex items-center justify-center shadow">
            <i class="fas fa-dove text-white text-sm"></i>
          </div>
          <span class="font-black text-slate-900 text-base tracking-tight">
            CPCT<span class="text-primary-light">-Youth</span>
          </span>
        </div>
        <h2 class="text-2xl font-black text-slate-900 mb-1">Join the Movement</h2>
        <p class="text-xs text-slate-400 mb-8">
          Register your profile to coordinate your professional expertise and skills with the youth peaceful struggle.
        </p>

        <!-- Success state -->
        <div v-if="success"
          class="flex flex-col items-center text-center gap-4 py-12">
          <div class="w-16 h-16 bg-green-50 rounded-2xl flex items-center justify-center">
            <i class="fas fa-check-circle text-primary text-3xl"></i>
          </div>
          <h3 class="text-xl font-black text-slate-900">Profile Submitted</h3>
          <p class="text-xs text-slate-500 max-w-sm leading-relaxed">
            Your profile has been successfully received by the committee. A regional coordinator will verify and activate your account shortly.
          </p>
          <button @click="$emit('close')"
            class="mt-4 px-8 py-3 bg-primary hover:bg-slate-900 text-white font-bold
                   rounded-xl transition-all text-xs uppercase tracking-wider">
            Close Panel
          </button>
        </div>

        <!-- Registration form -->
        <form v-else @submit.prevent="register" class="space-y-6">
          
          <!-- Outer dynamic grid container: single column on mobile, balanced two columns on large screens -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            
            <!-- Left Grid Column -->
            <div class="space-y-6">
              
              <!-- SECTION 1: Personal Information -->
              <div class="rounded-2xl border border-slate-100 p-5 space-y-4 bg-white shadow-sm">
                <p class="text-[10px] font-black uppercase tracking-[0.2em] text-primary">
                  Personal Details
                </p>

                <div class="grid grid-cols-2 gap-3">
                  <div>
                    <label class="field-label">First Name *</label>
                    <input v-model="form.first_name" type="text" required placeholder="Given name"
                      class="field-input" />
                  </div>
                  <div>
                    <label class="field-label">Last Name *</label>
                    <input v-model="form.last_name" type="text" required placeholder="Family name"
                      class="field-input" />
                  </div>
                </div>

                <div class="grid grid-cols-2 gap-3">
                  <div>
                    <label class="field-label">Age *</label>
                    <input v-model.number="form.age" type="number" min="15" max="45" required
                      placeholder="Years" class="field-input" />
                  </div>
                  <div>
                    <label class="field-label">Gender *</label>
                    <select v-model="form.gender" required class="field-input bg-slate-50">
                      <option value="">Select</option>
                      <option value="male">Male</option>
                      <option value="female">Female</option>
                    </select>
                  </div>
                </div>

                <div>
                  <label class="field-label">Location / City *</label>
                  <input v-model="form.location" type="text" required
                    placeholder="Current city or region"
                    class="field-input" />
                </div>
              </div>

              <!-- SECTION 2: Contact Details -->
              <div class="rounded-2xl border border-slate-100 p-5 space-y-4 bg-white shadow-sm">
                <p class="text-[10px] font-black uppercase tracking-[0.2em] text-primary">Communications</p>

                <div>
                  <label class="field-label">Email Address *</label>
                  <input v-model="form.email" type="email" required placeholder="username@domain.com"
                    class="field-input" />
                </div>

                <div>
                  <label class="field-label">Phone Number <span class="text-slate-400 lowercase font-normal">(optional)</span></label>
                  <input v-model="form.phone" type="tel" placeholder="Include country code"
                    class="field-input" />
                </div>
              </div>
            </div>

            <!-- Right Grid Column -->
            <div class="space-y-6">
              
              <!-- SECTION 3: Professional Background -->
              <div class="rounded-2xl border border-slate-100 p-5 space-y-4 bg-white shadow-sm">
                <p class="text-[10px] font-black uppercase tracking-[0.2em] text-primary">
                  Professional Profile
                </p>

                <div>
                  <label class="field-label">Profession / Occupation *</label>
                  <input v-model="form.profession" type="text" required
                    placeholder="Primary occupation"
                    class="field-input" />
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                  <div>
                    <label class="field-label">Highest Education *</label>
                    <select v-model="form.education" required class="field-input bg-slate-50">
                      <option value="">Select</option>
                      <option>High School</option>
                      <option>Diploma / TVET</option>
                      <option>Bachelor's Degree</option>
                      <option>Master's Degree</option>
                      <option>PhD / Doctorate</option>
                    </select>
                  </div>
                  <div>
                    <label class="field-label">Specialization <span class="text-slate-400 lowercase font-normal">(optional)</span></label>
                    <input v-model="form.field_of_study" type="text"
                      placeholder="Field of study"
                      class="field-input" />
                  </div>
                </div>
              </div>

              <!-- SECTION 4: Skills & Commitments -->
              <div class="rounded-2xl border border-slate-100 p-5 space-y-4 bg-white shadow-sm">
                <p class="text-[10px] font-black uppercase tracking-[0.2em] text-primary">
                  Capabilities &amp; Availability
                </p>

                <div>
                  <label class="field-label">Core Skills * <span class="text-slate-400 lowercase font-normal">(comma-separated)</span></label>
                  <textarea v-model="form.skills" required rows="2"
                    placeholder="e.g. Translation, Logistics, Organizing"
                    class="field-input resize-none h-14"></textarea>
                </div>

                <div>
                  <label class="field-label">Contribution Goals <span class="text-slate-400 lowercase font-normal">(optional)</span></label>
                  <textarea v-model="form.aspirations" rows="1"
                    placeholder="Briefly state your movement objectives"
                    class="field-input resize-none h-10"></textarea>
                </div>

                <div>
                  <label class="field-label">General Availability *</label>
                  <select v-model="form.availability" required class="field-input bg-slate-50">
                    <option value="">Select</option>
                    <option value="full_time">Full-time Engagement</option>
                    <option value="part_time">Part-time Engagement</option>
                    <option value="weekends">Weekends Only</option>
                    <option value="remote_only">Remote / Digital Only</option>
                    <option value="as_needed">As Needed / Urgent Calls</option>
                  </select>
                </div>
              </div>
            </div>
          </div>

          <!-- SECTION 5: Profile Photo & Account Security (Spans Full Width Below Columns) -->
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 pt-2 border-t border-slate-100">
            
            <!-- Photo Upload Box -->
            <div class="rounded-2xl border border-slate-100 p-5 flex items-center gap-4 bg-white shadow-sm">
              <div class="w-12 h-12 rounded-xl bg-slate-50 border border-slate-200 flex items-center justify-center overflow-hidden shrink-0">
                <img v-if="photoPreview" :src="photoPreview" alt="preview" class="w-full h-full object-cover" />
                <i v-else class="fas fa-user text-slate-300 text-lg"></i>
              </div>
              <div class="flex-1">
                <p class="text-[10px] font-black uppercase tracking-[0.2em] text-primary mb-1">Identification Photo</p>
                <input ref="photoInput" @change="handlePhoto" type="file" accept="image/*" class="hidden" id="photo-upload" />
                <label for="photo-upload"
                  class="cursor-pointer inline-flex items-center gap-2 px-3 py-1.5 bg-slate-50 border border-slate-200 hover:border-primary/40 rounded-lg text-[11px] font-bold text-slate-700 transition-all">
                  <i class="fas fa-upload text-[9px]"></i>
                  Select Image File
                </label>
              </div>
            </div>

            <!-- Security Credentials Box -->
            <div class="rounded-2xl border border-slate-100 p-5 space-y-3 bg-white shadow-sm">
              <p class="text-[10px] font-black uppercase tracking-[0.2em] text-primary">Security Credentials</p>
              <div class="grid grid-cols-2 gap-3">
                <div>
                  <label class="field-label">Password *</label>
                  <input v-model="form.password" type="password" required placeholder="Minimum 6 chars" class="field-input" />
                </div>
                <div>
                  <label class="field-label">Confirm *</label>
                  <input v-model="form.confirm_password" type="password" required placeholder="Verify password" class="field-input" />
                </div>
              </div>
            </div>
          </div>

          <!-- Consent Checkbox -->
          <label class="flex items-start gap-3 cursor-pointer group px-1">
            <input v-model="form.consent" type="checkbox" required
              class="mt-0.5 w-4 h-4 rounded border-slate-300 text-primary focus:ring-primary/20 cursor-pointer shrink-0" />
            <span class="text-[11px] text-slate-500 leading-relaxed group-hover:text-slate-700 transition-colors">
              I authorize the coordinating committee to retain my profile details strictly for structured operations within the peaceful resistance movement. Data remains confidential and fully protected. *
            </span>
          </label>

          <!-- Error Alert Panel -->
          <div v-if="error"
            class="flex items-start gap-2 bg-red-50 border border-red-100 text-red-600 px-4 py-3 rounded-xl text-xs font-semibold">
            <i class="fas fa-exclamation-circle mt-0.5 shrink-0"></i>
            {{ error }}
          </div>

          <!-- Form Control Actions -->
          <button type="submit" :disabled="loading || !form.consent"
            class="w-full py-4 bg-primary hover:bg-slate-900 disabled:opacity-50 text-white font-bold rounded-xl text-xs uppercase tracking-[0.2em] transition-all duration-300 shadow-lg shadow-primary/10 flex items-center justify-center gap-3">
            <i v-if="loading" class="fas fa-spinner animate-spin text-xs"></i>
            {{ loading ? 'Processing Registration...' : 'Submit Profile Application' }}
            <i v-if="!loading" class="fas fa-arrow-right text-xs"></i>
          </button>
        </form>

        <!-- Dynamic Modal Switch Links -->
        <p class="text-center text-xs text-slate-400 mt-6">
          Registered member?
          <button @click="$emit('switch-to-login')"
            class="text-primary hover:text-slate-900 font-bold ml-1 transition-colors">
            Sign In Here
          </button>
        </p>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RegisterModal',
  emits: ['close', 'switch-to-login'],

  data() {
    return {
      loading:      false,
      success:      false,
      error:        '',
      photoPreview: null,

      form: {
        first_name:     '',
        last_name:      '',
        age:            null,
        gender:         '',
        location:       '',
        email:          '',
        phone:          '',
        profession:     '',
        education:      '',
        field_of_study: '',
        skills:         '',
        aspirations:    '',
        availability:   '',
        photo:          null,
        password:          '',
        confirm_password:  '',
        consent: false,
      },
    };
  },

  methods: {
    handlePhoto(event) {
      const file = event.target.files[0];
      if (!file) return;
      if (file.size > 5 * 1024 * 1024) {
        this.error = 'Photo size must not exceed 5 MB.';
        this.$refs.photoInput.value = '';
        return;
      }
      this.form.photo   = file;
      this.photoPreview = URL.createObjectURL(file);
      this.error        = '';
    },

    async register() {
      this.error = '';

      if (this.form.password !== this.form.confirm_password) {
        this.error = 'Input passwords do not match.'; return;
      }
      if (this.form.password.length < 6) {
        this.error = 'Password must be 6 characters or longer.'; return;
      }
      if (!this.form.consent) {
        this.error = 'Operational data consent is mandatory.'; return;
      }

      this.loading = true;
      try {
        const fd = new FormData();
        fd.append('first_name',     this.form.first_name);
        fd.append('last_name',      this.form.last_name);
        fd.append('age',            this.form.age);
        fd.append('gender',         this.form.gender);
        fd.append('location',       this.form.location);
        fd.append('email',          this.form.email);
        fd.append('phone',          this.form.phone);
        fd.append('profession',     this.form.profession);
        fd.append('education',      this.form.education);
        fd.append('field_of_study', this.form.field_of_study);
        fd.append('skills',         this.form.skills);
        fd.append('aspirations',    this.form.aspirations);
        fd.append('availability',   this.form.availability);
        fd.append('password',       this.form.password);
        fd.append('consent',        true);
        if (this.form.photo) fd.append('photo', this.form.photo);

        await this.$apiPost('/auth/register', fd, { 'Content-Type': 'multipart/form-data' });
        this.success = true;
      } catch (err) {
        this.error =
          err?.response?.data?.error   ||
          err?.response?.data?.detail  ||
          err?.response?.data?.message ||
          err?.message                 ||
          'Network request failed. Please resubmit.';
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>

<script setup>
// If utilizing specific icon sets or modular builds inside Vue
</script>

<style scoped>
.field-label {
  @apply block text-[10px] font-black text-slate-500 mb-1.5 uppercase tracking-wider;
}
.field-input {
  @apply w-full px-4 py-2.5 border border-slate-200 bg-slate-50 rounded-xl text-xs
         focus:outline-none focus:ring-2 focus:ring-primary/10 focus:border-primary
         transition-all placeholder:text-slate-400 font-semibold text-slate-900;
}
</style>
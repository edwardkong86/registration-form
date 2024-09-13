<template>
  <div class="app">
    <h2>Member Registration</h2>
    <!-- Progress Indicator (Optional) -->
    <div class="progress-bar" :style="{ width: `${progress}%` }"></div>

    <!-- Step 1 and Step 2 Form Components -->
    <transition name="fade">
      <StepOne v-if="currentStep === 1" :formData="formData" @next-step="goToStep2" />
    </transition>
    <transition name="fade">
      <StepTwo v-if="currentStep === 2" :formData="formData" @submit-form="submitForm" />
    </transition>
  </div>
</template>

<script>
import StepOne from './RegistrationFormStepOne.vue';
import StepTwo from './RegistrationFormStepTwo.vue';

export default {
  data() {
    return {
      currentStep: 1,
      formData: {
        name: '',
        surname: '',
        username: '',
        email: '',
        password: '',
        confirmPassword: '',
        idNumber: '',
        telephone: '',
        securityQuestion: '',
        securityAnswer: '',
        loginMethod: '',
        acceptTerms: false
      }
    };
  },
  components: {
    StepOne,
    StepTwo
  },
  computed: {
    progress() {
      return this.currentStep === 1 ? 50 : 100;
    }
  },
  methods: {
    goToStep2(formData) {
    this.formData = { ...this.formData, ...formData }
      this.currentStep = 2;
    },
    submitForm(formData) {
      this.formData = { ...this.formData, ...formData }
      console.log('Final Form Data:', this.formData);
      alert('Registration Successful!');
    }
  }
};
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: 50px auto;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.progress-bar {
  height: 5px;
  background-color: #4caf50;
  margin-bottom: 20px;
  transition: width 0.3s ease-in-out;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>

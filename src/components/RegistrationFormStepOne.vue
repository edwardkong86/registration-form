<template>
  <div class="form-container">
    <form @submit.prevent="nextStep">
      <!-- Name and Surname -->
      <div class="form-row">
        <div class="form-group">
        <div class="form-cell-row">
          <i class="fas fa-id-card"></i>
          <input type="text" v-model="localFormData.name" placeholder="Your name" required />
          </div>
        </div>
        <div class="form-group">
        <div class="form-cell-row">
          <i class="fas fa-id-card"></i>
          <input type="text" v-model="localFormData.surname" placeholder="Your surname" required />
        </div>
        </div>
      </div>

      <!-- Username and Email -->
      <div class="form-row">
        <div class="form-group">
          <div class="form-cell-row">
          <i class="fas fa-user"></i>
          <input type="text" v-model="localFormData.username" placeholder="Your username" required />
          </div>
        </div>
        <div class="form-group">
          <div class="form-cell-row">
          <i class="fas fa-envelope"></i>
          <input type="email" v-model="localFormData.email" placeholder="E-mail" required />
          </div>
        </div>
      </div>

      <!-- Password and Confirm Password -->
      <div class="form-row">
        <div class="form-group">
          <div class="form-cell-row">
          <i class="fas fa-lock"></i>
          <input :type="showPassword ? 'text' : 'password'" v-model="localFormData.password" placeholder="Your password" required />
          <div @click="togglePassword()">
            <span v-if="showPassword">
              <i class="fas fa-eye"></i>
            </span>
            <span v-else>
              <i class="fas fa-eye-slash"></i>
            </span>
          </div>
          </div>
        </div>
        <div class="form-group">
          <div class="form-cell-row">
          <i class="fas fa-lock"></i>
          <input :type="showPassword ? 'text' : 'password'" v-model="localFormData.confirmPassword" placeholder="Reenter password" required />
          <div @click="togglePassword()">
            <span v-if="showPassword">
              <i class="fas fa-eye"></i>
            </span>
            <span v-else>
              <i class="fas fa-eye-slash"></i>
            </span>
          </div>
          </div>
        </div>
      </div>

      <!-- Next Step Button -->
      <button type="submit" class="btn-primary">GO TO NEXT STEP</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      localFormData: {
        name: '',
        surname: '',
        username: '',
        email: '',
        password: '',
        confirmPassword: ''
      },
      showPassword: false
    };
  },
  methods: {
    togglePassword() {
      this.showPassword = !this.showPassword;
    },
    nextStep() {
      if (this.localFormData.password !== this.localFormData.confirmPassword) {
        alert("Passwords don't match");
        return;
      }
      // Proceed to the next step
      console.log(this.localFormData);
      this.$emit('next-step', this.localFormData);
    }
  }
};
</script>

<style scoped>
.form-container {
  background-color: #f8f9fa;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

.form-row {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  margin-bottom: 10px;
}

.form-cell-row {
  display: flex;
  justify-content: space-between;
}

.form-group {
  flex: 1;
  position: relative;
}

input {
  width: 100%;
  padding: 10px 15px;
  border-radius: 25px;
  border: 1px solid #ccc;
  font-size: 14px;
  padding-left: 40px; /* For icon space */
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

input:focus {
  border-color: #4caf50;
  box-shadow: 0 0 5px rgba(76, 175, 80, 0.5);
}

svg.svg-inline--fa {
  position: absolute;
  top: 50%;
  left: 10px;
  transform: translateY(-50%);
  font-size: 18px;
  color: #555;
}

svg.svg-inline--fa.fa-eye,
svg.svg-inline--fa.fa-eye-slash {
  right: 10px;
  left: auto;
  cursor: pointer;
}

button.btn-primary {
  width: 100%;
  padding: 12px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 25px;
  font-size: 16px;
  cursor: pointer;
  margin-top: 20px;
}

button.btn-primary:hover {
  background-color: #45a049;
}

@media (max-width: 768px) {
  .form-row {
    flex-direction: column;
  }
}
</style>

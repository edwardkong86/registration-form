<template>
  <div class="form-container">
    <form @submit.prevent="submitForm">
      <!-- Identification Number and Telephone -->
      <div class="form-row">
        <div class="form-group">
          <div class="form-cell-row">
            <i class="fas fa-id-card"></i>
            <input
              type="text"
              v-model="localFormData.idNumber"
              placeholder="Identification Number"
              required
            />
          </div>
        </div>
        <div class="form-group">
          <div class="form-cell-row">
            <i class="fas fa-mobile-alt"></i>
            <input
              type="text"
              v-model="localFormData.telephone"
              placeholder="Telephone"
              required
            />
          </div>
        </div>
      </div>

      <!-- Security Question and Answer -->
      <div class="form-row">
        <div class="form-group">
          <div class="form-cell-row">
            <i class="fas fa-shield-alt"></i>
            <input
              type="text"
              v-model="localFormData.securityQuestion"
              placeholder="Security Question"
              required
            />
          </div>
        </div>
        <div class="form-group">
          <div class="form-cell-row">
            <i class="fas fa-lock"></i>
            <input
              type="text"
              v-model="localFormData.securityAnswer"
              placeholder="Security Answer"
              required
            />
          </div>
        </div>
      </div>

      <!-- Login Setup Menu -->
      <div class="login-setup">
        <h3>LOGIN SETUP MENU</h3>
        <div class="login-body">
        <div class="form-row">
          <div class="form-group">
            <div class="form-cell-row selection">
            <div @click="toggleLoginSetup('email')" class="email">
              <span v-if="localFormData.loginMethod == 'email'">
                <CircleDotSvg />
              </span>
              <span v-else>
                <CircleSvg />
              </span>
            </div>
            <label for="emailLogin">Activate login via email</label>
            </div>
          </div>
          <div class="form-group">
            <div class="form-cell-row selection">
            <div @click="toggleLoginSetup('sms')" class="hexagon">
              <span v-if="localFormData.loginMethod == 'sms'">
                <CircleDotSvg />
              </span>
              <span v-else>
                <CircleSvg />
              </span>
            </div>
            <label for="smsLogin">Activate login via SMS</label>
            </div>
          </div>
          <div class="form-group">
            <div class="form-cell-row selection">
             <div @click="toggleLoginSetup('disabled')" class="hexagon">
              <span v-if="localFormData.loginMethod == 'disabled'">
                <CircleDotSvg />
              </span>
              <span v-else>
                <CircleSvg />
              </span>
            </div>
            <label for="disableLogin">Disable all</label>
            </div>
          </div>
        </div>
        </div>
      </div>

      <!-- Terms and Conditions -->
      <div class="terms-group">
        <div @click="toggleTerms()" class="hexagon">
          <span v-if="localFormData.acceptTerms">
            <HexagonCheckSvg />
          </span>
          <span v-else>
            <HexagonSvg />
          </span>
        </div>
        <label class="terms-label" for="terms">I HAVE READ AND ACCEPT THE GENERAL TERMS AND CONDITIONS</label>
      </div>

      <!-- Submit Button -->
      <button
        type="submit"
        class="btn-primary"
        :disabled="!localFormData.acceptTerms"
      >
        REGISTER NOW
      </button>
    </form>
  </div>
</template>

<script>
import HexagonCheckSvg from "@/components/HexagonCheckSvg.vue";
import HexagonSvg from "@/components/HexagonSvg.vue";
import CircleDotSvg from "@/components/CircleDotSvg.vue";
import CircleSvg from "@/components/CircleSvg.vue";

export default {
  components: {HexagonCheckSvg, HexagonSvg, CircleDotSvg, CircleSvg},
  props: ["formData"],
  data() {
    return {
      localFormData: {
          "idNumber": "",
          "telephone": "",
          "securityQuestion": "",
          "securityAnswer": "",
          "loginMethod": "email",
          "acceptTerms": false
      },
    };
  },
  methods: {
    toggleLoginSetup(value) {
      this.localFormData.loginMethod = value;
    },
    toggleTerms() {
      this.localFormData.acceptTerms = !this.localFormData.acceptTerms;
    },
    submitForm() {
      if (!this.localFormData.acceptTerms) {
        alert("Please accept the terms and conditions.");
        return;
      }
      console.log("submitForm", this.localFormData);
      this.$emit("submit-form", this.localFormData);
    },
  },
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

.form-cell-row.selection {
  display: flex;
  justify-content: left;
}

.form-group {
  position: relative;
  flex: 1;
  margin: 0 5px;
}

input[type="text"],
input[type="radio"],
input[type="checkbox"] {
  width: 100%;
  padding: 10px 15px;
  border-radius: 25px;
  border: 1px solid #ccc;
  padding-left: 40px;
  font-size: 14px;
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

.terms-label {
margin-left:10px;
}

.login-setup {
  background-color: #e0e0e0;
  padding: 15px;
  border-radius: 10px;
  margin-top: 20px;
}
.login-body {
  background-color: #FFFFFF;
  margin:-15px;
  margin-top:-5px;
  padding:15px;
  border-radius: 10px;
}

h3 {
  margin-top:0px;
  font-size: 18px;
  color: #333;
  text-align: center;
}

input[type="radio"] {
  margin-right: 10px;
}

.form-group label {
  margin-left: 10px;
}

.terms-group {
  display: flex;
  align-items: center;
  margin: 20px 0;
}

input[type="checkbox"] {
  margin-right: 10px;
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
}

button.btn-primary:disabled {
  background-color: gray;
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

<template>
  <div>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Nom :</label>
        <input 
          type="text" 
          id="name" 
          v-model="name" 
          @blur="validateName" 
          :class="{ invalid: errors.name }" 
        />
        <span v-if="errors.name" class="error">{{ errors.name }}</span>
      </div>

      <div>
        <label for="email">Email :</label>
        <input 
          type="email" 
          id="email" 
          v-model="email" 
          @blur="validateEmail" 
          :class="{ invalid: errors.email }" 
        />
        <span v-if="errors.email" class="error">{{ errors.email }}</span>
      </div>

      <div>
        <label for="phone">Numéro de téléphone :</label>
        <input 
          type="tel" 
          id="phone" 
          v-model="phone" 
          @blur="validatePhone" 
          :class="{ invalid: errors.phone }" 
        />
        <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
      </div>

      <button type="submit">Soumettre</button>
    </form>
    
    <div v-if="submitted" class="confirmation">
      <p>Formulaire soumis avec succès !</p>
      <p><strong>Nom :</strong> {{ name }}</p>
      <p><strong>Email :</strong> {{ email }}</p>
      <p><strong>Téléphone :</strong> {{ phone }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserForm",
  data() {
    return {
      name: "",
      email: "",
      phone: "",
      errors: {
        name: null,
        email: null,
        phone: null
      },
      submitted: false
    };
  },
  methods: {
    validateName() {
      if (!this.name) {
        this.errors.name = "Le nom est requis.";
      } else {
        this.errors.name = null;
      }
    },
    validateEmail() {
      const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
      if (!this.email) {
        this.errors.email = "L'email est requis.";
      } else if (!emailPattern.test(this.email)) {
        this.errors.email = "Veuillez entrer un email valide.";
      } else {
        this.errors.email = null;
      }
    },
    validatePhone() {
      const phonePattern = /^[0-9]{10}$/;
      if (!this.phone) {
        this.errors.phone = "Le numéro de téléphone est requis.";
      } else if (!phonePattern.test(this.phone)) {
        this.errors.phone = "Veuillez entrer un numéro de téléphone valide (10 chiffres).";
      } else {
        this.errors.phone = null;
      }
    },
    submitForm() {
      this.validateName();
      this.validateEmail();
      this.validatePhone();

      if (!this.errors.name && !this.errors.email && !this.errors.phone) {
        this.submitted = true;
      }
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin: auto;
}

div {
  margin-bottom: 15px;
}

label {
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

input.invalid {
  border-color: red;
}

.error {
  color: red;
  font-size: 0.9em;
}

button {
  padding: 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.confirmation {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #4CAF50;
  border-radius: 4px;
  background-color: #f0f9f0;
}
</style>

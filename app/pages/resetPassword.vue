<template>
  <div class="reset-password-container">
    <div class="reset-password-card">
      <h2>Réinitialisation du mot de passe</h2>
      <p class="description">Veuillez entrer votre nouveau mot de passe ci-dessous.</p>
      
      <form @submit.prevent="handleResetPassword" class="reset-form">
        <div class="form-group">
          <label for="password">Nouveau mot de passe</label>
          <input 
            id="password" 
            v-model="password" 
            type="password" 
            required 
            placeholder="Votre nouveau mot de passe"
          />
        </div>
        
        <div class="form-group">
          <label for="confirmPassword">Confirmer le mot de passe</label>
          <input 
            id="confirmPassword" 
            v-model="confirmPassword" 
            type="password" 
            required 
            placeholder="Confirmez le mot de passe"
          />
        </div>
        
        <div v-if="errorMsg" class="message error">{{ errorMsg }}</div>
        <div v-if="successMsg" class="message success">{{ successMsg }}</div>

        <button type="submit" :disabled="loading" class="submit-btn">
          {{ loading ? 'Mise à jour...' : 'Réinitialiser mon mot de passe' }}
        </button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const supabase = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();

const password = ref('');
const confirmPassword = ref('');
const loading = ref(false);
const errorMsg = ref('');
const successMsg = ref('');

onMounted(() => {
  // Optionnel : on peut détecter spécifiquement l'événement de récupération
  supabase.auth.onAuthStateChange((event, session) => {
    if (event == 'PASSWORD_RECOVERY') {
      console.log('Mode récupération de mot de passe activé.');
    }
  });
});

const handleResetPassword = async () => {
  errorMsg.value = '';
  successMsg.value = '';

  if (password.value !== confirmPassword.value) {
    errorMsg.value = "Les mots de passe ne correspondent pas.";
    return;
  }

  // Vérification de sécurité locale
  if (!user.value) {
    errorMsg.value = "Aucune session de récupération trouvée. Veuillez utiliser le lien valide reçu par email.";
    return;
  }

  loading.value = true;
  
  try {
    const { error } = await supabase.auth.updateUser({
      password: password.value
    });

    if (error) {
      throw error;
    }
    
    successMsg.value = "Votre mot de passe a été réinitialisé avec succès !";
    password.value = '';
    confirmPassword.value = '';
    
    setTimeout(() => {
      router.push('/');
    }, 2500);
    
  } catch (error: any) {
    errorMsg.value = error.message || "Une erreur inattendue est survenue.";
  } finally {
    loading.value = false;
  }
};
</script>

<style scoped>
.reset-password-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
  background-color: var(--background-color, #f9fafb);
  font-family: inherit;
}

.reset-password-card {
  background: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05), 0 10px 15px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
}

h2 {
  margin-top: 0;
  margin-bottom: 8px;
  color: #111827;
  font-size: 24px;
  text-align: center;
}

.description {
  text-align: center;
  color: #6b7280;
  margin-bottom: 24px;
  font-size: 14px;
}

.reset-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

label {
  font-size: 14px;
  font-weight: 500;
  color: #374151;
}

input {
  padding: 10px 12px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 14px;
  transition: border-color 0.2s, box-shadow 0.2s;
}

input:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25);
}

.submit-btn {
  margin-top: 8px;
  padding: 12px;
  background-color: #0f172a;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 15px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.submit-btn:hover:not(:disabled) {
  background-color: #1e293b;
}

.submit-btn:disabled {
  background-color: #9ca3af;
  cursor: not-allowed;
}

.message {
  padding: 10px 12px;
  border-radius: 6px;
  font-size: 14px;
  margin-top: 4px;
}

.error {
  background-color: #fef2f2;
  color: #b91c1c;
  border: 1px solid #fecaca;
}

.success {
  background-color: #f0fdf4;
  color: #15803d;
  border: 1px solid #bbf7d0;
}
</style>
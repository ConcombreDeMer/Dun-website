<template>
    <div class="reset-password-container">

        <img width="200px" src="/images/7.png" alt="Illustration de réinitialisation du mot de passe" class="illustration" />

        <div class="reset-password-card">
            <h2>Réinitialisation du mot de passe</h2>
            <p class="description">Veuillez entrer votre nouveau mot de passe ci-dessous.</p>

            <form @submit.prevent="handleResetPassword" class="reset-form">
                <div class="form-group">
                    <label for="password">Nouveau mot de passe</label>
                    <input id="password" v-model="password" type="password" required
                        placeholder="Votre nouveau mot de passe" />
                </div>

                <div class="form-group">
                    <label for="confirmPassword">Confirmer le mot de passe</label>
                    <input id="confirmPassword" v-model="confirmPassword" type="password" required
                        placeholder="Confirmez le mot de passe" />
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
import { ref, onMounted, watch } from 'vue';
import { useRouter, useRoute } from 'vue-router';

const supabase = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();
const route = useRoute();

const password = ref('');
const confirmPassword = ref('');
const loading = ref(false);
const errorMsg = ref('');
const successMsg = ref('');

onMounted(async () => {
    console.log("URL complète au chargement:", window.location.href);

    // Parfois Nuxt Supabase a besoin d'un petit moment pour traiter le "#access_token" dans l'URL
    // On écoute les changements d'état d'authentification
    supabase.auth.onAuthStateChange(async (event, session) => {
        console.log("Événement d'authentification Supabase:", event);
        if (session) {
            console.log("Session récupérée avec succès !");
        }
    });

    // Gestion du flow PKCE au cas où
    if (route.query.code) {
        const { error } = await supabase.auth.exchangeCodeForSession(String(route.query.code));
        if (error) console.error("Erreur exchangeCodeForSession:", error.message);
    }
});

const handleResetPassword = async () => {
    errorMsg.value = '';
    successMsg.value = '';

    if (password.value !== confirmPassword.value) {
        errorMsg.value = "Les mots de passe ne correspondent pas.";
        return;
    }

    loading.value = true;

    try {
        // Si la session n'est toujours pas montée mais qu'on a un access_token dans l'URL (Implicit Flow)
        const hash = window.location.hash;
        let accessTokenParts = hash.match(/access_token=([^&]+)/);

        if (accessTokenParts && accessTokenParts[1]) {
            // On force la mise à jour directement avec l'access token de l'URL si besoin (fallback)
            await supabase.auth.setSession({
                access_token: accessTokenParts[1],
                refresh_token: hash.match(/refresh_token=([^&]+)/)?.[1] || ''
            });
        }

        // Mise à jour du mot de passe
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
            router.push('/'); // Ou vers votre page de login
        }, 2500);

    } catch (error: any) {
        errorMsg.value = error.message || "Une erreur inattendue est survenue.";
    } finally {
        loading.value = false;
    }
};
</script>

<style scoped>
@font-face {
    font-family: 'MaFont';
    src: url('/fonts/Satoshi-Variable.ttf') format('truetype');
}

.reset-password-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 20px;
    background-color: #f5f5f5;
    font-family: 'MaFont', sans-serif;
    color: #1a1a1a;
    flex-direction: column;
    
}

.reset-password-card {
    background: white;
    padding: 40px;
    border-radius: 16px;
    border: 1px solid #e8e8e8;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.05);
    width: 100%;
    max-width: 440px;
    box-sizing: border-box;
    margin-bottom: 200px;
}

h2 {
    margin-top: 0;
    margin-bottom: 12px;
    color: #1a1a1a;
    font-size: 28px;
    text-align: center;
    font-weight: 700;
}

.description {
    text-align: center;
    color: #666;
    margin-bottom: 30px;
    font-size: 16px;
    line-height: 1.5;
}

.reset-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

label {
    font-size: 14px;
    font-weight: 600;
    color: #1a1a1a;
}

input {
    padding: 14px 16px;
    border: 1px solid #e0e0e0;
    border-radius: 12px;
    font-size: 16px;
    font-family: 'MaFont', sans-serif;
    transition: all 0.3s ease;
    background-color: #fafafa;
    color: #1a1a1a;
}

input:focus {
    outline: none;
    border-color: #1a1a1a;
    background-color: white;
}

input::placeholder {
    color: #999;
}

.submit-btn {
    margin-top: 10px;
    padding: 14px 24px;
    background-color: #1a1a1a;
    color: white;
    border: none;
    border-radius: 12px;
    font-size: 16px;
    font-weight: 600;
    font-family: 'MaFont', sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
}

.submit-btn:hover:not(:disabled) {
    background-color: #333;
    transform: translateY(-2px);
}

.submit-btn:active:not(:disabled) {
    transform: translateY(0);
}

.submit-btn:disabled {
    background-color: #e0e0e0;
    color: #999;
    cursor: not-allowed;
    transform: none;
}

.message {
    padding: 12px 16px;
    border-radius: 10px;
    font-size: 14px;
    text-align: center;
    font-weight: 500;
    margin-top: 8px;
}

.error {
    background-color: rgba(255, 107, 107, 0.1);
    color: #ff6b6b;
    border: 1px solid rgba(255, 107, 107, 0.3);
}

.success {
    background-color: rgba(144, 238, 144, 0.1);
    color: #2e8b57;
    border: 1px solid rgba(144, 238, 144, 0.3);

.illustration {
    width: 200px;
    max-width: 100%;
    margin-bottom: 24px;
}

/* Mobile Responsive Adjustments */
@media (max-width: 600px) {
    .reset-password-container {
        padding: 16px;
    }

    .reset-password-card {
        padding: 24px;
    }

    h2 {
        font-size: 24px;
        margin-bottom: 8px;
    }

    .description {
        font-size: 14px;
        margin-bottom: 20px;
    }

    .illustration {
        width: 150px;
        margin-bottom: 16px;
    }

    input {
        padding: 12px 14px;
        font-size: 15px;
    }

    .submit-btn {
        margin-top: 5px;
        padding: 12px 20px;
        font-size: 15px;
    }
}
}
</style>
<template>
  <div class="success-page">
    <!-- Header -->
    <header class="header">
      <div class="container">
        <NuxtLink to="/" class="logo-link">
          <div class="logo">
            <div class="logo-icon">✓</div>
            <span>Dun</span>
          </div>
        </NuxtLink>
      </div>
    </header>

    <!-- Success Content -->
    <div class="success-container">
      <div class="success-content">
        <!-- Checkmark Animation -->
        <div class="success-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
            <polyline points="22 4 12 14.01 9 11.01" />
          </svg>
        </div>

        <!-- Confirmation Message -->
        <h1 class="success-title">Bienvenue sur Dun!</h1>
        
        <p class="success-subtitle">
          Ton email a été confirmé avec succès
        </p>

        <div class="confirmation-box">
          <p>Tu fais maintenant partie de la bêta fermée de Dun. Prépare-toi à révolutionner ta productivité 🚀</p>
        </div>

        <!-- Next Steps -->
        <div class="next-steps">
          <h2>Ce qui se passe ensuite</h2>
          
          <div class="steps-list">
            <div class="step">
              <div class="step-number">1</div>
              <div class="step-content">
                <h3>Retourne sur ton app</h3>
                <p>Retourne sur ton app Dun et connecte toi avec l'email que tu viens de confirmer</p>
              </div>
            </div>

            <div class="step">
              <div class="step-number">2</div>
              <div class="step-content">
                <h3>Organise ta journée</h3>
                <p>Commence à planifier et atteindre tes objectifs avec Dun</p>
              </div>
            </div>

            <div class="step">
              <div class="step-number">3</div>
              <div class="step-content">
                <h3>Partage tes retours</h3>
                <p>Aide-nous à améliorer Dun en partageant tes commentaires et suggestions</p>
              </div>
            </div>
          </div>
        </div>

        <!-- CTA Buttons -->
        <div class="actions">
          <button v-if="isNativeApp" @click="openApp" class="button button-primary">
            Ouvrir dans l'app Dun
          </button>
          <NuxtLink v-if="!isNativeApp" to="/" class="button button-primary">
            Retour à l'accueil
          </NuxtLink>
          <a href="mailto:contact@dun.app" class="button button-secondary">
            Nous contacter
          </a>
        </div>

        <!-- Footer Message -->
        <p class="footer-message">
          Merci d'avoir rejoint notre communauté. Voyons ensemble comment Dun peut transformer ta productivité.
        </p>
      </div>
    </div>

    <!-- Background Decoration -->
    <div class="background-decoration"></div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';

const isNativeApp = ref(false);
const appOpened = ref(false);

onMounted(() => {
  document.querySelector('.success-page')?.classList.add('loaded');
  
  // Détection du système (iOS/Android)
  const userAgent = navigator.userAgent;
  const isIOS = /iPad|iPhone|iPod/.test(userAgent);
  const isAndroid = /Android/.test(userAgent);
  
  if (isIOS) {
    isNativeApp.value = true;
    
    // Essayer d'ouvrir l'app iOS avec le custom URL scheme
    const deepLinkTimeout = setTimeout(() => {
      try {
        window.location.href = 'dun://successMail';
      } catch (e) {
        // Si ça échoue, rester sur la page web
        console.log('App not available');
      }
    }, 500);
    
    // Nettoyer le timeout si la page est quittée
    return () => clearTimeout(deepLinkTimeout);
  } else if (isAndroid) {
    isNativeApp.value = true;
  }
});

const openApp = () => {
  try {
    window.location.href = 'dun://successMail';
  } catch (e) {
    console.error('Erreur lors de l\'ouverture de l\'app:', e);
  }
};
</script>

<style lang="scss" scoped>
.success-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #ffffff 0%, #fafafa 100%);
  font-family: 'MaFont', sans-serif;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;

  &.loaded {
    .success-icon {
      animation: iconPop 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }

    .success-title {
      animation: slideIn 0.8s ease-out 0.2s both;
    }

    .success-subtitle {
      animation: slideIn 0.8s ease-out 0.3s both;
    }

    .confirmation-box {
      animation: slideIn 0.8s ease-out 0.4s both;
    }

    .next-steps {
      animation: slideIn 0.8s ease-out 0.5s both;
    }

    .actions {
      animation: slideIn 0.8s ease-out 0.6s both;
    }
  }
}

@keyframes iconPop {
  0% {
    transform: scale(0) rotate(-45deg);
    opacity: 0;
  }
  70% {
    transform: scale(1.15);
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Header */
.header {
  padding: 20px 0;
  border-bottom: 1px solid #f0f0f0;
  background-color: white;
  position: relative;
  z-index: 10;

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .logo-link {
    text-decoration: none;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 24px;
    font-weight: 700;
    color: #1a1a1a;
    transition: all 0.3s ease;
    cursor: pointer;

    &:hover {
      transform: scale(1.05);
    }

    .logo-icon {
      width: 40px;
      height: 40px;
      background-color: #1a1a1a;
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-size: 20px;
    }
  }
}

/* Success Container */
.success-container {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 60px 20px;
  position: relative;
  z-index: 5;
}

.success-content {
  max-width: 600px;
  text-align: center;
  background: white;
  padding: 60px 40px;
  border-radius: 24px;
  border: 1px solid #e8e8e8;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.05);
}

/* Success Icon */
.success-icon {
  width: 80px;
  height: 80px;
  margin: 0 auto 40px;
  background: linear-gradient(135deg, #1a1a1a 0%, #333 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;

  svg {
    width: 50px;
    height: 50px;
    stroke: white;
  }
}

/* Success Title */
.success-title {
  font-size: 40px;
  font-weight: 700;
  margin-bottom: 16px;
  color: #1a1a1a;
  line-height: 1.2;
}

.success-subtitle {
  font-size: 18px;
  color: #666;
  margin-bottom: 40px;
  line-height: 1.6;
}

/* Confirmation Box */
.confirmation-box {
  background: linear-gradient(135deg, #f5f5f5 0%, #e8e8e8 100%);
  padding: 30px 25px;
  border-radius: 16px;
  margin-bottom: 50px;
  border-left: 4px solid #1a1a1a;

  p {
    font-size: 16px;
    color: #333;
    line-height: 1.6;
    margin: 0;
  }
}

/* Next Steps */
.next-steps {
  margin-bottom: 50px;
  text-align: left;

  h2 {
    font-size: 24px;
    font-weight: 700;
    margin-bottom: 30px;
    text-align: center;
    color: #1a1a1a;
  }
}

.steps-list {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.step {
  display: flex;
  gap: 20px;
  align-items: flex-start;
}

.step-number {
  width: 48px;
  height: 48px;
  background-color: #1a1a1a;
  color: white;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 18px;
  flex-shrink: 0;
}

.step-content {
  flex: 1;

  h3 {
    font-size: 16px;
    font-weight: 600;
    margin-bottom: 6px;
    color: #1a1a1a;
  }

  p {
    font-size: 14px;
    color: #666;
    margin: 0;
    line-height: 1.5;
  }
}

/* Actions */
.actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-bottom: 40px;

  @media (max-width: 480px) {
    gap: 12px;
  }
}

.button {
  padding: 16px 32px;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  font-family: 'MaFont', sans-serif;
  text-decoration: none;
  display: inline-block;
  transition: all 0.3s ease;
  cursor: pointer;
  border: none;

  &:hover {
    transform: translateY(-2px);
  }

  &:active {
    transform: translateY(0);
  }
}

.button-primary {
  background-color: #1a1a1a;
  color: white;

  &:hover {
    background-color: #333;
  }
}

.button-secondary {
  background-color: white;
  color: #1a1a1a;
  border: 2px solid #1a1a1a;

  &:hover {
    background-color: #f5f5f5;
  }
}

/* Footer Message */
.footer-message {
  font-size: 14px;
  color: #999;
  line-height: 1.6;
  margin: 0;
}

/* Background Decoration */
.background-decoration {
  position: fixed;
  top: -50%;
  right: -10%;
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(26, 26, 26, 0.05) 0%, transparent 70%);
  border-radius: 50%;
  pointer-events: none;
  z-index: 1;
}

/* Responsive */
@media (max-width: 768px) {
  .success-content {
    padding: 40px 24px;
  }

  .success-title {
    font-size: 28px;
  }

  .success-subtitle {
    font-size: 16px;
  }

  .confirmation-box {
    margin-bottom: 40px;
    padding: 24px 20px;
  }

  .next-steps h2 {
    font-size: 20px;
  }

  .next-steps {
    margin-bottom: 40px;
  }

  .actions {
    margin-bottom: 30px;
  }
}

@media (max-width: 480px) {
  .success-page {
    padding-top: 10px;
  }

  .success-container {
    padding: 40px 16px;
  }

  .success-content {
    padding: 32px 20px;
    border-radius: 16px;
  }

  .success-icon {
    width: 64px;
    height: 64px;
    margin-bottom: 30px;

    svg {
      width: 40px;
      height: 40px;
    }
  }

  .success-title {
    font-size: 24px;
    margin-bottom: 12px;
  }

  .success-subtitle {
    font-size: 14px;
    margin-bottom: 30px;
  }

  .confirmation-box {
    margin-bottom: 30px;
    padding: 20px 16px;

    p {
      font-size: 14px;
    }
  }

  .step {
    gap: 16px;
  }

  .step-number {
    width: 40px;
    height: 40px;
    font-size: 16px;
  }

  .step-content {
    h3 {
      font-size: 15px;
    }

    p {
      font-size: 13px;
    }
  }
}
</style>

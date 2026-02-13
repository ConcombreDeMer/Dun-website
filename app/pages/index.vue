<template>
  <div class="dun-landing">
    <NuxtRouteAnnouncer />
    
    <!-- Header -->
    <header class="header">
      <div class="container header-content">
        <div class="logo">
          <div class="logo-icon">✓</div>
          <span>Dun</span>
        </div>
        <button @click="scrollToBeta" class="beta-button">Rejoindre la bêta fermée</button>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <div class="container">
        <h1 class="hero-title">Organise ta journée</h1>
        <p class="hero-subtitle">La productivité simplifiée. Planifie simplement, atteins tes objectifs.</p>
        
        <!-- Mockup -->
        <div class="mockup-container-hero">
          <img 
            src="/mockups/1.png" 
            alt="Mockup de l'application Dun" 
            class="mockup-image"
          />
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="features">
      <div class="container">
        <h2 class="section-title">Pourquoi choisir Dun?</h2>
        
        <div class="features-grid">
          <div class="feature-card">
            <div class="feature-icon">✓</div>
            <h3>Simple à utiliser</h3>
            <p>Une interface épurée pour rester concentré sur ce qui compte vraiment</p>
          </div>
          
          <div class="feature-card">
            <div class="feature-icon">📅</div>
            <h3>Planifie facilement</h3>
            <p>Vue journalière, hebdomadaire pour une organisation parfaite</p>
          </div>
          
          <div class="feature-card">
            <div class="feature-icon">🎯</div>
            <h3>Atteins tes objectifs</h3>
            <p>Suivi de ta progression et statistiques pour rester motivé</p>
          </div>
          
          <div class="feature-card">
            <div class="feature-icon">⚙️</div>
            <h3>Ton espace personnel</h3>
            <p>Personnalise l'affichage et l'expérience selon tes préférences</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Screenshots Section -->
    <section class="screenshots">
      <div class="container">
        <h2 class="section-title">Découvre l'interface</h2>
        
        <div class="screenshots-grid">
          <div class="screenshot-card">
            <div class="screenshot-placeholder">
              <div class="placeholder-text">Écran Affichage</div>
            </div>
          </div>
          
          <div class="screenshot-card">
            <div class="screenshot-placeholder">
              <div class="placeholder-text">Écran Tâches</div>
            </div>
          </div>
          
          <div class="screenshot-card">
            <div class="screenshot-placeholder">
              <div class="placeholder-text">Écran Statistiques</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Beta Signup Section -->
    <section class="beta-signup" id="beta-section">
      <div class="container">
        <div class="signup-content">
          <h2>Rejoins la bêta fermée</h2>
          <p>Sois parmi les premiers à essayer Dun et façonne le futur de la productivité</p>
          
          <form @submit.prevent="handleSignup" class="signup-form">
            <div class="form-group">
              <input 
                v-model="email" 
                type="email" 
                placeholder="Ton email"
                required
                class="email-input"
              />
              <button type="submit" class="signup-button" :disabled="loading">
                {{ loading ? 'En attente...' : 'Rejoindre' }}
              </button>
            </div>
            
            <div v-if="successMessage" class="success-message">
              {{ successMessage }}
            </div>
            <div v-if="errorMessage" class="error-message">
              {{ errorMessage }}
            </div>
          </form>
          
          <p class="privacy-note">Aucune donnée personnelle ne sera partagée</p>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-section">
            <h4>Dun</h4>
            <p>La productivité simplifiée</p>
          </div>
          
          <div class="footer-section">
            <h4>Liens</h4>
            <ul>
              <li><a href="#beta">Bêta</a></li>
              <li><a href="#contact">Contact</a></li>
            </ul>
          </div>
        </div>
        
        <div class="footer-bottom">
          <p>&copy; 2026 Dun. Tous droits réservés.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const email = ref('');
const loading = ref(false);
const successMessage = ref('');
const errorMessage = ref('');

const scrollToBeta = () => {
  const betaSection = document.getElementById('beta-section');
  if (betaSection) {
    betaSection.scrollIntoView({ behavior: 'smooth' });
  }
};

const handleSignup = async () => {
  if (!email.value) {
    errorMessage.value = 'Veuillez renseigner votre email';
    return;
  }

  loading.value = true;
  successMessage.value = '';
  errorMessage.value = '';

  try {
    // Simuler l'envoi du formulaire
    // À remplacer par votre vrai API endpoint
    await new Promise(resolve => setTimeout(resolve, 1000));
    
    successMessage.value = 'Merci! Vérifie ton email pour confirmer ton inscription.';
    email.value = '';
    
    setTimeout(() => {
      successMessage.value = '';
    }, 5000);
  } catch (error) {
    errorMessage.value = 'Une erreur est survenue. Réessaye plus tard.';
  } finally {
    loading.value = false;
  }
};
</script>

<style lang="scss">
@font-face {
  font-family: 'MaFont';
  src: url('/fonts/Satoshi-Variable.ttf') format('truetype');
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  font-family: 'MaFont', sans-serif;
  background-color: #ffffff;
  color: #1a1a1a;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

// Header
.header {
  padding: 20px 0;
  border-bottom: 1px solid #f0f0f0;
  position: sticky;
  top: 0;
  background-color: white;
  z-index: 100;

  .header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 24px;
    font-weight: 700;

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

.beta-button {
  padding: 12px 24px;
  background-color: #1a1a1a;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 14px;
  font-weight: 600;
  font-family: 'MaFont', sans-serif;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;

  &:hover {
    background-color: #333;
    transform: scale(1.05);
  }

  &:active {
    transform: scale(0.98);
  }

  @media (max-width: 640px) {
    padding: 10px 16px;
    font-size: 12px;
  }
}

// Hero Section
.hero {
  padding: 120px 0 80px;
  text-align: center;

  .hero-title {
    font-size: 56px;
    font-weight: 700;
    margin-bottom: 20px;
    line-height: 1.2;
  }

  .hero-subtitle {
    font-size: 20px;
    color: #666;
    margin-bottom: 60px;
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
  }
}

.mockup-container-hero {
  display: flex;
  justify-content: center;
}

.mockup-placeholder,
.screenshot-placeholder {
  background: linear-gradient(135deg, #f5f5f5 0%, #e8e8e8 100%);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid #e0e0e0;
  transition: all 0.3s ease;

  .placeholder-text {
    color: #999;
    font-size: 16px;
    font-weight: 500;
  }

  &:hover {
    border-color: #1a1a1a;
    background: linear-gradient(135deg, #fafafa 0%, #f0f0f0 100%);
  }
}

.mockup-container-hero .mockup-placeholder {
  width: 100%;
  max-width: 500px;
  height: 400px;
}

.mockup-container-hero .mockup-image {
  width: 100%;
  max-width: 500px;
  height: auto;
  border-radius: 20px;
  transition: all 0.3s ease;
  display: block;

  &:hover {
    box-shadow: 0 15px 50px rgba(0, 0, 0, 0.15);
    transform: translateY(-5px);
  }
}

// Features Section
.features {
  padding: 100px 0;
  background-color: #fafafa;

  .section-title {
    font-size: 40px;
    font-weight: 700;
    margin-bottom: 60px;
    text-align: center;
  }

  .features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 40px;
  }

  .feature-card {
    background-color: white;
    padding: 40px 30px;
    border-radius: 16px;
    border: 1px solid #e8e8e8;
    text-align: center;
    transition: all 0.3s ease;

    &:hover {
      border-color: #1a1a1a;
      transform: translateY(-5px);
    }

    .feature-icon {
      font-size: 40px;
      margin-bottom: 20px;
    }

    h3 {
      font-size: 18px;
      font-weight: 600;
      margin-bottom: 12px;
    }

    p {
      font-size: 14px;
      color: #666;
      line-height: 1.6;
    }
  }
}

// Screenshots Section
.screenshots {
  padding: 100px 0;

  .section-title {
    font-size: 40px;
    font-weight: 700;
    margin-bottom: 60px;
    text-align: center;
  }

  .screenshots-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
  }

  .screenshot-card {
    .screenshot-placeholder {
      width: 100%;
      height: 500px;
    }
  }
}

// Beta Signup Section
.beta-signup {
  padding: 100px 0;
  background-color: #1a1a1a;
  color: white;

  .signup-content {
    max-width: 600px;
    margin: 0 auto;
    text-align: center;

    h2 {
      font-size: 40px;
      font-weight: 700;
      margin-bottom: 20px;
    }

    > p {
      font-size: 18px;
      color: #ccc;
      margin-bottom: 40px;
    }
  }

  .signup-form {
    margin-bottom: 30px;
  }

  .form-group {
    display: flex;
    gap: 12px;
    margin-bottom: 20px;

    @media (max-width: 640px) {
      flex-direction: column;
    }
  }

  .email-input {
    flex: 1;
    padding: 16px 20px;
    border: 1px solid #444;
    border-radius: 12px;
    background-color: #2a2a2a;
    color: white;
    font-size: 16px;
    font-family: 'MaFont', sans-serif;
    transition: all 0.3s ease;

    &::placeholder {
      color: #888;
    }

    &:focus {
      outline: none;
      border-color: white;
      background-color: #333;
    }
  }

  .signup-button {
    padding: 16px 40px;
    background-color: white;
    color: #1a1a1a;
    border: none;
    border-radius: 12px;
    font-size: 16px;
    font-weight: 600;
    font-family: 'MaFont', sans-serif;
    cursor: pointer;
    transition: all 0.3s ease;
    white-space: nowrap;

    &:hover:not(:disabled) {
      background-color: #f0f0f0;
      transform: scale(1.02);
    }

    &:disabled {
      opacity: 0.7;
      cursor: not-allowed;
    }
  }

  .success-message {
    color: #90ee90;
    font-size: 16px;
    padding: 12px 20px;
    background-color: rgba(144, 238, 144, 0.1);
    border-radius: 8px;
    border: 1px solid rgba(144, 238, 144, 0.3);
  }

  .error-message {
    color: #ff6b6b;
    font-size: 16px;
    padding: 12px 20px;
    background-color: rgba(255, 107, 107, 0.1);
    border-radius: 8px;
    border: 1px solid rgba(255, 107, 107, 0.3);
  }

  .privacy-note {
    font-size: 13px;
    color: #999;
  }
}

// Footer
.footer {
  padding: 60px 0 20px;
  background-color: #f5f5f5;
  border-top: 1px solid #e8e8e8;

  .footer-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 40px;
    margin-bottom: 40px;
  }

  .footer-section {
    h4 {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 12px;
    }

    p {
      font-size: 14px;
      color: #666;
    }

    ul {
      list-style: none;

      li {
        margin-bottom: 8px;

        a {
          font-size: 14px;
          color: #666;
          text-decoration: none;
          transition: color 0.3s ease;

          &:hover {
            color: #1a1a1a;
          }
        }
      }
    }
  }

  .footer-bottom {
    padding-top: 20px;
    border-top: 1px solid #e8e8e8;
    text-align: center;

    p {
      font-size: 12px;
      color: #999;
    }
  }
}

// Responsive
@media (max-width: 768px) {
  .hero-title {
    font-size: 36px;
  }

  .hero-subtitle {
    font-size: 18px;
  }

  .section-title {
    font-size: 28px;
  }

  .beta-signup h2 {
    font-size: 28px;
  }
}
</style>
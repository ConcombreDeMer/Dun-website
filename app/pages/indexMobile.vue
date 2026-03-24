<template>
  <div class="container">

    <div class="titles">
      <h1 class="title">Dun</h1>
      <h2 class="subtitle">Prends le contrôle <br>de tes journées</h2>
    </div>

    <div class="char-container">
      <img src="/images/1.png" alt="Hero Image" class="char" />
    </div>

    <div class="dispo">
      <p class="dispo-text">Beta disponible</p>
    </div>

    <img src="/images/chevron-down.png" alt="Hero Image" class="chevron" />


    <div class="card">
      <h2 class="card-title">Simple</h2>
      <p class="card-desc">
        Des fonctionnalités sans <span class="bold">superflu</span> avec une gestion de tâches et un agenda qui va <span
          class="bold">droit au but</span>.
      </p>
      <img src="/images/list.png" alt="Hero Image" class="card-img" />
    </div>

    <div class="card">
      <h2 class="card-title">Analytique</h2>
      <p class="card-desc">
        Des <span class="bold">statistiques</span> pour suivre ton évolutions ainsi que des <span class="bold">conseils
          et astuces</span> afin de réaliser tes objectifs.
      </p>
      <img src="/images/graph.png" alt="Hero Image" class="card-img" />
    </div>

    <div class="card">
      <h2 class="card-title">Customisable</h2>
      <p class="card-desc">
        Une application qui <span class="bold">s’adapte</span> à toi et pas l’inverse à travers une personnalisation de
        <span class="bold">l’interface</span> et de <span class="bold">la
          gestion de tâches</span>.
      </p>
      <img src="/images/custom.png" alt="Hero Image" class="card-img" />
    </div>


    <div class="beta">
      <h2 class="beta-title">Inscris toi</h2>
      <h2 class="beta-title2">à la beta fermée</h2>
      <p class="beta-desc">
        Pour être parmi les premiers à utiliser
        Dun et nous aider à façonner des apps
        qui reviennent à l’essentiel.
      </p>
      <!-- <img src="/images/beta.png" alt="Hero Image" class="card-img" /> -->
      <input type="email" placeholder="Entres ton email" class="email-input" />

      <a href="/" class="join">
        Rejoindre
      </a>

    </div>


  </div>

</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>

.join {
  background-color: #000000;
  color: #ffffff;
  padding: 12px 30px;
  border-radius: 15px;
  font-family: 'Satoshi-Medium', sans-serif;
  font-size: 16px;
  margin-top: 20px;
  text-decoration: none;
  margin-bottom: 80px;
}


.email-input {
  width: 300px;
  height: 48px;
  border-radius: 15px;
  border: none;
  padding: 0 20px;
  font-size: 16px;
  font-family: 'Satoshi-Regular', sans-serif;
  margin-top: 20px;
  width: 80%;
  background-color: #717171;
  border: 1px solid #A7A7A7;
}

.beta {
  background-color: #474747;
  color: #ffffff;
  padding-top: 50px;
  padding-bottom: 50px;
  margin-top: 50px;
  position: relative;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
}

.beta-title2 {
  font-size: 24px;
  font-family: 'Satoshi-Black', sans-serif;
  color: #ffffff;
  padding: 0;
  margin: 0;
  text-align: center;
  opacity: 0.65;
}

.beta-title {
  font-size: 38px;
  font-family: 'Satoshi-Black', sans-serif;
  color: #ffffff;
  padding: 0;
  margin: 0;
  text-align: center;
}

.beta-desc {
  font-size: 18px;
  color: #ffffff;
  font-family: 'Satoshi-Regular', sans-serif;
  line-height: 1.2;
  padding-left: 20px;
  padding-right: 20px;
  margin: 0;
  margin-top: 80px;
  text-align: flex-start;
}


.card-img {
  width: 18%;
  margin-top: 5%;
  position: absolute;
  right: 30px;
  bottom: 30px;
  opacity: 0.9;
}


.bold {
  font-family: 'Satoshi-Bold', sans-serif;
}


.card-desc {
  font-size: 1.25rem;
  color: #646464;
  font-family: 'Satoshi-Regular', sans-serif;
  line-height: 1.2;
  padding-left: 20px;
  padding-right: 20px;
  margin: 0;
  margin-top: 20px;
}

.card-title {
  font-size: 2rem;
  font-family: 'Satoshi-Black', sans-serif;
  color: #000000;
  padding: 0;
  margin: 0;
  margin-top: 10%;
  text-align: center;
}


.card {
  width: 80%;
  height: 80vw;
  background-color: #ffffff;
  margin-top: 50px;
  margin-left: auto;
  margin-right: auto;
  border-radius: 40px;
  border: 1px solid #e0e0e0;
  position: relative;
}

.container {
  justify-content: start;
  flex-direction: column;
  font-family: 'Satoshi-Regular', sans-serif;
}

.titles {
  text-align: flex-start;
  margin-left: 5%;
  margin-top: 10%;
}

.title {
  font-size: 96px;
  font-family: 'Satoshi-Black', sans-serif;
  color: #000000;
  padding: 0;
  margin: 0;
}

.subtitle {
  font-size: 1.5rem;
  color: #868686;
  font-family: 'Satoshi-Bold', sans-serif;
  line-height: 1;
  padding: 0;
  margin: 0;
}

.char-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.char {
  width: 60%;
  margin-top: 5%;
  margin-left: auto;
  margin-right: auto;
}

.dispo {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 100px;
  background-color: #474747;
  width: 200px;
  height: 48px;
  border-radius: 15px;
  margin-left: auto;
  margin-right: auto;
}

.dispo-text {
  color: #ffffff;
  font-family: 'Satoshi-Medium', sans-serif;
  font-size: 16px;
}

.chevron {
  display: block;
  margin: 50px auto 0 auto;
  width: 24px;
  opacity: 0.5;
}
</style>
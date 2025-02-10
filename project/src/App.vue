<template>
  <div id="container">
    <div id="left-panel">
      <!-- name -->
      <div class="field">
        <label for="name">Name</label>
        <input id="name" type="text" placeholder="Name" v-model="name" />
      </div>
      <!-- job -->
      <div class="field">
        <label for="job">Job</label>
        <input id="job" type="text" placeholder="Job" v-model="job" />
      </div>
      <!-- contact -->
      <!-- langues -->
      <div class="field">
        <label for="langues">Langues</label>
        <input id="langues" type="text" placeholder="Langues" v-model="langues" />
      </div>
      <!-- projets -->
      <!-- interests -->
      <div class="field">
        <label for="interest">Interests</label>
        <div v-for="(item, index) in interests" :key="index">
          <input v-model="item.value" placeholder="Entrer une valeur" />
          <button @click="removeInterest(index)">Remove</button>
        </div>
        <button @click="addInterest">Add interest</button>
      </div>

      <button id="generate-pdf" @click="generatePDF">Générer le PDF</button>
    </div>
    <div id="right-panel">
      <div id="cv">
        <div id="left-panel-cv">
          <section class="head sub-section">
            <h1>{{ name }}</h1>
            <h2>{{job}}</h2>
          </section>
          <div>
            <section class="sub-section">
              <h3 class="section-title">CONTACT</h3>
              <p class="link">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="lucide lucide-phone"
                >
                  <path
                    d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"
                  />
                </svg>
                <span>06.89.01.20.66</span>
              </p>
              <p class="link">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="lucide lucide-mail"
                >
                  <rect width="20" height="16" x="2" y="4" rx="2" />
                  <path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7" />
                </svg>
                <a href="mailto:michaelbecquer@protonmail.com"
                  >michaelbecquer@protonmail.com</a
                >
              </p>
              <p class="link">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="lucide lucide-linkedin"
                >
                  <path
                    d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"
                  />
                  <rect width="4" height="12" x="2" y="9" />
                  <circle cx="4" cy="4" r="2" />
                </svg>
                <a
                  href="https://linkedin.com/in/michaël-becquer-7750a731a"
                  target="_blank"
                  >linkedin.com/in/michaël-becquer-7750a731a</a
                >
              </p>
              <p class="link">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="lucide lucide-github"
                >
                  <path
                    d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"
                  />
                  <path d="M9 18c-4.51 2-5-2-7-2" />
                </svg>
                <a href="https://github.com/MiKL-B" target="_blank"
                  >github.com/MiKL-B</a
                >
              </p>
            </section>
            <section class="sub-section">
              <h3 class="section-title">LANGUES</h3>
              <p>Anglais</p>
            </section>
            <section class="sub-section">
              <h3 class="section-title">PROJETS REALISES</h3>
              <p class="link">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="lucide lucide-briefcase-business"
                >
                  <path d="M12 12h.01" />
                  <path d="M16 6V4a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2" />
                  <path d="M22 13a18.15 18.15 0 0 1-20 0" />
                  <rect width="20" height="14" x="2" y="6" rx="2" />
                </svg>
                <span>Portfolio:</span>
                <a href="https://mikl-b.github.io" target="_blank"
                  >mikl-b.github.io</a
                >
              </p>
              <p class="link">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="lucide lucide-coffee"
                >
                  <path d="M10 2v2" />
                  <path d="M14 2v2" />
                  <path
                    d="M16 8a1 1 0 0 1 1 1v8a4 4 0 0 1-4 4H7a4 4 0 0 1-4-4V9a1 1 0 0 1 1-1h14a4 4 0 1 1 0 8h-1"
                  />
                  <path d="M6 2v2" />
                </svg>
                <span>Fika CSS:</span>
                <a href="https://fika-css.vercel.app" target="_blank"
                  >fika-css.vercel.app</a
                >
              </p>
            </section>
            <section class="sub-section">
              <h3 class="section-title">CENTRES D'INTERET</h3>
              <ul>
                <li v-for="(interest, index) in interests" :key="index">
                  {{ interest.value }}
                </li>
              </ul>
            </section>
          </div>
        </div>
        <div id="right-panel-cv">
          <p class="text-profile">
            Développeur web frontend junior passionné par les technologies web,
            doté de compétences en HTML, CSS et JavaScript, ainsi que d'une
            expérience en Vue.js, prêt à participer à des projets innovants au
            sein d'une équipe dynamique.
          </p>
          <section>
            <h3 class="section-title">EXPERIENCE PROFESSIONNELLE</h3>
            <div class="sub-section">
              <h4>ANALYSTE PROGRAMMEUR - COMPUSOFT LUNEVILLE</h4>
              <p class="date">septembre 2022 - janvier 2025</p>
              <ul>
                <li>Développement d'applications ou de modules.</li>
                <li>Maintenance d'applications ou de modules existants.</li>
                <li>Assistance à la clientèle.</li>
                <li>
                  Analyse des besoins des clients de la société Compusoft.
                </li>
              </ul>
            </div>
            <div class="sub-section">
              <h4>ANALYSTE PROGRAMMEUR STAGIAIRE - COMPUSOFT LUNEVILLE</h4>
              <p class="date">mai 2022 - juillet 2022</p>
              <ul>
                <li>Maquettage d'un composant de l'application.</li>
                <li>
                  Développement de l'interface, des composants métiers, ainsi
                  que des composants d'accès aux données.
                </li>
                <li>
                  Collaboration à la gestion d'un projet informatique et à
                  l'organisation de l'environnement de développement.
                </li>
              </ul>
            </div>
            <div class="sub-section">
              <h4>
                DÉVELOPPEUR WEB STAGIAIRE - ASSOCIATION KYOSAI TELETRAVAIL
              </h4>
              <p class="date">mars 2021 - mai 2021</p>
              <ul>
                <li>Maquettage de l'application.</li>
                <li>
                  Développement de l'interface utilisateur web dynamique avec
                  une solution de gestion de contenu et e-commerce.
                </li>
                <li>
                  Développement de la partie backend de l'application, ainsi que
                  des composants d'accès aux données.
                </li>
              </ul>
              <ul>
                <li>
                  <a
                    href="https://github.com/MiKL-B/kyosai-front/tree/develop/kyosai-front"
                    >github.com/MiKL-B/kyosai-front/tree/develop/kyosai-front</a
                  >
                </li>
                <li>
                  <a
                    href="https://github.com/MiKL-B/kyosai-back/tree/develop/kyosai-back"
                    >github.com/MiKL-B/kyosai-back/tree/develop/kyosai-back</a
                  >
                </li>
              </ul>
            </div>
          </section>
          <section>
            <h3 class="section-title">FORMATION</h3>
            <div class="sub-section">
              <h4>CONCEPTEUR DÉVELOPPEUR D'APPLICATIONS - AFPA FROUARD</h4>
              <p class="date">septembre 2021 - juillet 2022</p>
              <p>Titre professionnel de Niveau 6 (Bac +4)</p>
            </div>
            <div class="sub-section">
              <h4>DÉVELOPPEUR WEB / WEB MOBILE - AFPA FROUARD</h4>
              <p class="date">septembre 2020 - juillet 2021</p>
              <p>Titre professionnel de Niveau 5 (Bac +2)</p>
            </div>
          </section>
          <section>
            <h3 class="section-title">COMPETENCES</h3>
            <div>
              <ul>
                <li>
                  Conception de maquettes fonctionnelles pour les applications
                  web et mobiles.
                </li>
                <li>
                  Conception d'interface utilisateur web dynamique responsive.
                </li>
                <li>
                  Connaissances en technologies web modernes frontend (HTML5,
                  CSS3, JavaScript, Vue.js, TailwindCSS) et backend (Node.js).
                </li>
                <li>Méthodes d'intégration API RESTful.</li>
                <li>
                  Conception de la base de données et développement des
                  composants d'accès aux données.
                </li>
                <li>Utilisation de bibliothèques de test (Cypress, Jest).</li>
                <li>Outil de contrôle de versions Git.</li>
                <li>Application de la méthode Agile (Scrum, Kanban).</li>
                <li>
                  Connaissances des principes d'accessibilité web, du SEO, ainsi
                  que des bonnes pratiques de développement frontend.
                </li>
              </ul>
            </div>
          </section>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "Michaël BECQUER",
      job:"DEVELOPPEUR WEB FRONTEND",
      interests: [
        { value: "Lecture" },
        { value: "Peinture" },
        { value: "Cuisine" },
        { value: "Voyages" },
        { value: "Taekwondo" },
        { value: "Moto" },
        { value: "Veille technologique" },
      ],
      year: new Date().getFullYear(),
      extension: ".pdf",
      CVName: "CV_Michaël_BECQUER_" + this.year + this.extension,
    };
  },
  methods: {
    addInterest() {
      this.interests.push({ value: "" });
    },
    removeInterest(index) {
      this.interests.splice(index, 1);
    },
    generatePDF() {
      const element = document.getElementById("cv");
      const opt = {
        //   margin: 0.5,
        filename: this.CVName,
        image: { type: "jpeg", quality: 0.98 },
        html2canvas: { scale: 2 },
        jsPDF: { unit: "cm", format: "a4", orientation: "portrait" },
      };

      // Générer le PDF
      html2pdf().from(element).set(opt).save();
    },
  },
};
</script>
<style>
body {
  overflow: hidden;
}
#container {
  display: flex;
  flex-wrap: wrap;
}

#left-panel {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  gap: 1rem;
}

#right-panel {
  height: 99vh;
  margin: auto;
  margin-top: 0.5rem;
  overflow-y: auto;
  border: 1px solid var(--grey);
}
.field {
  display: flex;
  flex-direction: column;
}
</style>

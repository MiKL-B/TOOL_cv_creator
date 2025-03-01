<template>
  <div id="container">
    <div id="left-panel">
      <!-- photo -->
     <!--  <div class="field">
        <label for="photo">Photo</label>
        <input type="file" @change="handleFileUpload" accept="image/*" />
      </div> -->
      <!-- name -->
      <div class="field">
        <label for="name">Name</label>
        <input id="name" type="text" placeholder="Name" v-model="name" />
      </div>
      <!-- firstname -->
      <div class="field">
        <label for="firstname">Firstname</label>
        <input
          id="firstname"
          type="text"
          placeholder="Firstname"
          v-model="firstname"
        />
      </div>
      <!-- job -->
      <div class="field">
        <label for="job">Job</label>
        <input id="job" type="text" placeholder="Job" v-model="job" />
      </div>
      <!-- contact -->
      <!-- languages -->
      <div class="field">
        <label for="languages">Langues</label>
        <div v-for="(item, index) in languages" :key="index">
          <input v-model="item.value" placeholder="Entrer une valeur" />
          <button @click="removeLanguage(index)">Remove</button>
        </div>
        <button @click="addLanguage">Add</button>
      </div>
      <!-- projets -->
      <div class="field">
        <label for="projects">Projects</label>
        <div v-for="(item, index) in projects" :key="index">
          <input v-model="item.label" placeholder="Entrer le nom" />
          <input v-model="item.link" placeholder="Entrer le lien" />
          <input v-model="item.value" placeholder="Entrer la valeur" />
          <button @click="removeProject(index)">Remove</button>
        </div>
        <button @click="addProject">Add</button>
      </div>
      <!-- hard skills -->
      <div class="field">
        <label for="hardskills">Hard skills</label>
        <div v-for="(item, index) in hardskills" :key="index">
          <input v-model="item.value" placeholder="Entrer la valeur" />
          <button @click="removeHardSkill(index)">Remove</button>
        </div>
        <button @click="addHardSkill">Add</button>
      </div>
      <!-- soft skills -->
      <div class="field">
        <label for="softskills">Soft skills</label>
        <div v-for="(item, index) in softskills" :key="index">
          <input v-model="item.value" placeholder="Entrer la valeur" />
          <button @click="removeSoftSkill(index)">Remove</button>
        </div>
        <button @click="addSoftSkill">Add</button>
      </div>
      <!-- interests -->
      <div class="field">
        <label for="interest">Interests</label>
        <div v-for="(item, index) in interests" :key="index">
          <input v-model="item.value" placeholder="Entrer une valeur" />
          <button @click="removeInterest(index)">Remove</button>
        </div>
        <button @click="addInterest">Add</button>
      </div>

      <button id="generate-pdf" @click="generatePDF">Générer le PDF</button>
    </div>
    <!-- cv -->
    <div id="right-panel">
      <div id="cv">
        <div id="left-panel-cv">
          <section class="head sub-section">
            <div class="container-img">
              <div class="img">
                <img src="./assets/photo.png" />
                <!-- <img v-if="imageUrl" :src="imageUrl" /> -->
              </div>
            </div>
            <div>
              <!-- <h1>{{ name }}</h1> -->
              <h1 class="name">
                <span class="firstname">{{ firstname }}</span>
                <span>{{ name }}</span>
              </h1>
              <h2 class="job">{{ job }}</h2>
            </div>
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
                  >linkedin.com/in/michaelbecquer</a
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
                  class="lucide lucide-map-pin"
                >
                  <path
                    d="M20 10c0 4.993-5.539 10.193-7.399 11.799a1 1 0 0 1-1.202 0C9.539 20.193 4 14.993 4 10a8 8 0 0 1 16 0"
                  />
                  <circle cx="12" cy="10" r="3" />
                </svg>
                <span>54000 Nancy</span>
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
                  class="lucide lucide-car"
                >
                  <path
                    d="M19 17h2c.6 0 1-.4 1-1v-3c0-.9-.7-1.7-1.5-1.9C18.7 10.6 16 10 16 10s-1.3-1.4-2.2-2.3c-.5-.4-1.1-.7-1.8-.7H5c-.6 0-1.1.4-1.4.9l-1.4 2.9A3.7 3.7 0 0 0 2 12v4c0 .6.4 1 1 1h2"
                  />
                  <circle cx="7" cy="17" r="2" />
                  <path d="M9 17h6" />
                  <circle cx="17" cy="17" r="2" />
                </svg>
                <span>Permis B</span>
              </p>
            </section>
            <section class="sub-section">
              <h3 class="section-title">LANGUES</h3>

              <ul>
                <li v-for="(language, index) in languages" :key="index">
                  {{ language.value }}
                </li>
              </ul>
            </section>
            <section class="sub-section">
              <h3 class="section-title">PROJETS REALISES</h3>
              <ul>
                <li v-for="project in projects">
                  <span class="project">{{ project.label }}</span>
                  <a :href="project.link" target="_blank">{{
                    project.value
                  }}</a>
                </li>
              </ul>
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
            Développeur Frontend Vue.js. Passionné par les technologies web. Mes
            compétences en HTML, CSS et JavaScript sont complétées par une
            expérience significative avec Vue.js Je suis prêt à participer et
            mettre en oeuvre des projets innovants, de la conception à la mise
            en production, au sein d'une équipe dynamique.
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
                <li>Application de la méthode Agile (Scrum)</li>
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
                <li>Utilisation du système de gestion de version Git.</li>
                <li>Application de la méthode Agile (Scrum)</li>
              </ul>
            </div>
            <div class="sub-section">
              <h4>
                DÉVELOPPEUR WEB STAGIAIRE - ASSOCIATION KYOSAI TELETRAVAIL
              </h4>
              <p class="date">mars 2021 - mai 2021</p>
              <ul>
                <li>
                  Conception et intégration de la maquette pour le web et
                  mobiles.
                </li>
                <li>
                  Conception et développement de l'interface utilisateur web
                  dynamique et responsive, avec une solution de gestion de
                  contenu et e-commerce.
                </li>
                <li>Conception de la base de données.</li>
                <li>Développement de la partie backend.</li>
                <li>Développement des composants d'accès aux données.</li>
                <li>Mise en place des tests à l'aide du framework Cypress.</li>
                <li>Application de la méthode Agile (Kanban)</li>
              </ul>
              <div class="project-link">
                <a
                  href="https://github.com/MiKL-B/kyosai-front/tree/develop/kyosai-front"
                  >github.com/MiKL-B/kyosai-front/tree/develop/kyosai-front</a
                >
                <a
                  href="https://github.com/MiKL-B/kyosai-back/tree/develop/kyosai-back"
                  >github.com/MiKL-B/kyosai-back/tree/develop/kyosai-back</a
                >
              </div>
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
            <div class="skills">
              <ul>
                <li v-for="skill in hardskills">
                  {{ skill.value }}
                </li>
              </ul>
              <ul>
                <li v-for="skill in softskills">
                  {{ skill.value }}
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
      fileName: null,
      imageUrl: null,
      name: "BECQUER",
      firstname:"Michaël",
      job: "DEVELOPPEUR WEB FRONTEND",
      languages: [{ value: "Français" }, { value: "Anglais" }],
      projects: [
        {
          label: "Portfolio",
          link: "https://mikl-b.github.io",
          value: "mikl-b.github.io",
        },
        {
          label: "Site",
          link: "https://github.com/MiKL-B/ecommerce",
          value: "/MiKL-B/ecommerce",
        },
        {
          label: "Fika-CSS",
          link: "https://fika-css.vercel.app",
          value: "fika-css.vercel.app",
        },
      ],
      hardskills: [
        { value: "HTML5, CSS3,JavaScript(ES6)" },
        { value: "Vue.js, Vue router, Vuex / Pinia, Composition API" },
        { value: "TailwindCSS" },
        { value: "Node.js, npm, Vite" },
        { value: "Intégration API REST" },
        { value: "Responsive design" },
        { value: "Tests unitaires, E2E" },
        { value: "Git" },
        { value: "Accessibilité web" },
        { value: "SEO" },
      ],
      softskills: [
        { value: "Communication et collaboration" },
        { value: "Résolution de problèmes" },
        { value: "Esprit d'équipe" },
      ],
      interests: [
        { value: "Lecture" },
        { value: "Peinture" },
        { value: "Cuisine" },
        { value: "Voyages" },
        { value: "Taekwondo" },
        { value: "Moto" },
        { value: "Veille technologique" },
      ],

      CVName: "CV_Michaël_BECQUER",
    };
  },
  methods: {
    // photo
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        this.fileName = file.name; // On stocke le nom du fichier sélectionné
        this.imageUrl = URL.createObjectURL(file); // On crée l'URL de l'objet pour l'image
      } else {
        this.fileName = null;
        this.imageUrl = null; // Réinitialiser l'URL d'image si aucun fichier n'est sélectionné
      }
    },
    // language
    addLanguage() {
      this.languages.push({ value: "" });
    },
    removeLanguage(index) {
      this.languages.splice(index, 1);
    },
    // project
    addProject() {
      this.projects.push({ value: "" });
    },
    removeProject(index) {
      this.projects.splice(index, 1);
    },
    // hard skills
    addHardSkill() {
      this.hardskills.push({ value: "" });
    },
    removeHardSkill(index) {
      this.hardskills.splice(index, 1);
    },
    // soft skills
    addSoftSkill() {
      this.softskills.push({ value: "" });
    },
    removeSoftSkill(index) {
      this.softskills.splice(index, 1);
    },
    // interests
    addInterest() {
      this.interests.push({ value: "" });
    },
    removeInterest(index) {
      this.interests.splice(index, 1);
    },
    // pdf
    generatePDF() {
      const element = document.getElementById("cv");
      const opt = {
        //   margin: 0.5,
        filename: this.CVName,
        image: { type: "png", quality: 0.98 },
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

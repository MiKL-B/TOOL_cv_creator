<template>
  <div id="container">
    <button @click="isOpen = !isOpen">Menu</button>
    <div id="left-panel" v-if="isOpen">
      <h1>Profil</h1>
      <!-- photo -->
      <div class="field">
        <label for="photo">Photo</label>
        <input type="file" @change="handleFileUpload" accept="image/*" />
      </div>
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
      <h1>Contact</h1>
      <div class="field">
        <label for="tel">Telephone</label>
        <input type="tel" name="tel" id="tel" v-model="phone" />
      </div>
      <div class="field">
        <label for="email">Email</label>
        <input type="email" name="email" id="email" v-model="email" />
      </div>
      <div class="field">
        <label for="contactlinks">Links</label>
        <div
          name="contactlinks"
          v-for="(item, index) in contactLinks"
          :key="index"
        >
          <input v-model="item.value" placeholder="Entrer la valeur" />
          <input v-model="item.link" placeholder="Entrer le lien" />
          <button @click="removeContactLink(index)">Remove</button>
        </div>
        <button @click="addContactLink">Add</button>
      </div>
      <div class="field">
        <label for="address">Address</label>
        <input type="text" name="address" v-model="address" />
      </div>
      <!-- languages -->
      <h1>Langues</h1>
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
      <!-- Section -->
      <div class="field">
        <h1>Section</h1>
        <label for="sections">Sections</label>
        <div v-for="(section, index) in sections" :key="index">
          <input v-model="section.name" placeholder="Entrer une valeur" />
          <button @click="removeSection(index)">Remove section</button>

          <!--  -->
          <button @click="addSectionItem(section.list)">add Item</button>

          <select v-model="section.selectedType">
            <option :value="item" v-for="item in section.type" :key="index">
              {{ item }}
            </option>
          </select>
          <div v-for="(item, index) in section.list" :key="index">
            <input type="text" v-model="item.name" name="" />
            <select v-model="item.selectedType">
              <option
                :value="subitem"
                v-for="subitem in item.type"
                :key="index"
              >
                {{ subitem }}
              </option>
            </select>
            <button @click="removeSectionItem(section.list, index)">
              Remove item
            </button>
          </div>
        </div>
        <button @click="addSection">Add section</button>
      </div>
      <button id="generate-pdf" @click="generatePDF">Générer le PDF</button>
    </div>
    <!----------------------------- CV ------------------------------------>
    <div id="right-panel">
      <div id="cv">
        <div id="left-panel-cv">
          <section class="head sub-section">
            <div class="container-img" v-if="imageUrl">
              <div class="img">
                <img :src="imageUrl" />
              </div>
            </div>
            <div>
              <h1 class="name">
                <span class="firstname">{{ firstname }}</span>
                <span>{{ name }}</span>
              </h1>
              <h2 class="job">{{ job }}</h2>
            </div>
          </section>
          <div>
            <section id="sortable">
              <!-- contact -->
              <div class="sub-section sortable-section">
                <h3 class="section-title">CONTACT</h3>

                <p class="link" v-if="phone !== ''">
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
                  <span>{{ phone }}</span>
                </p>
                <p class="link" v-if="email !== ''">
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
                  <a :href="'mailto:' + email">{{ email }}</a>
                </p>
                <p class="link" v-for="item in contactLinks" :key="item.id">
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
                    class="lucide lucide-link"
                  >
                    <path
                      d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"
                    />
                    <path
                      d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"
                    />
                  </svg>
                  <a :href="item.link" target="_blank">{{ item.value }}</a>
                </p>

                <p class="link" v-if="address !== ''">
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
                  <span>{{ address }}</span>
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
              </div>
              <!-- langues -->
              <div class="sub-section sortable-section">
                <h3 class="section-title">LANGUES</h3>
                <ul>
                  <li v-for="(language, index) in languages" :key="index">
                    {{ language.value }}
                  </li>
                </ul>
              </div>
              <!-- projects -->
              <div class="sub-section sortable-section">
                <h3 class="section-title">PROJETS REALISES</h3>
                <ul>
                  <li v-for="project in projects">
                    <span class="project">{{ project.label }}</span>
                    <a :href="project.link" target="_blank">{{
                      project.value
                    }}</a>
                  </li>
                </ul>
              </div>
              <!-- interets -->
              <div class="sub-section sortable-section">
                <h3 class="section-title">CENTRES D'INTERET</h3>
                <ul>
                  <li v-for="(interest, index) in interests" :key="index">
                    {{ interest.value }}
                  </li>
                </ul>
              </div>
              <!-- sections -->
              <div
                class="sub-section sortable-section"
                v-for="section in sections"
                :key="section.id"
              >
                <h3 class="section-title">{{ section.name }}</h3>
                <ul v-if="section.selectedType === 'list'">
                  <li v-for="item in section.list">
                    <svg
                      v-if="item.selectedType === 'tel'"
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
                    {{ item.name }}
                  </li>
                </ul>
                <div v-else-if="section.selectedType === 'text'">
                  <p v-for="item in section.list">
                    <Phone v-if="item.selectedType === 'tel'" />
                    {{ item.name }}
                  </p>
                </div>
              </div>
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
          <section id="sortable1">
            <div class="sub-section sortable-section">
              <h3 class="section-title">EXPERIENCE PROFESSIONNELLE</h3>
              <!-- exp -->
              <div>
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
              <!-- exp -->
              <div>
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
              <!-- exp -->
              <div>
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
                  <li>
                    Mise en place des tests à l'aide du framework Cypress.
                  </li>
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
            </div>
            <!-- formations -->
            <div class="sub-section sortable-section">
              <div>
                <h3 class="section-title">FORMATION</h3>
                <h4>CONCEPTEUR DÉVELOPPEUR D'APPLICATIONS - AFPA FROUARD</h4>
                <p class="date">septembre 2021 - juillet 2022</p>
                <p>Titre professionnel de Niveau 6 (Bac +4)</p>
              </div>
              <div>
                <h4>DÉVELOPPEUR WEB / WEB MOBILE - AFPA FROUARD</h4>
                <p class="date">septembre 2020 - juillet 2021</p>
                <p>Titre professionnel de Niveau 5 (Bac +2)</p>
              </div>
            </div>
            <!-- skills -->
            <div class="sub-section sortable-section">
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
            </div>
          </section>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { Phone} from 'lucide-vue-next'
export default {
  name: "App",
  components:{
    Phone
  },
  data() {
    return {
      isOpen: false,
      fileName: null,
      imageUrl: null,
      // profil
      name: "",
      firstname: "",
      job: "",
      // contact
      phone: "",
      email: "",
      contactLinks: [],
      address: "",
      // language
      languages: [],
      projects: [],
      hardskills: [],
      softskills: [],
      interests: [],
      // sections
      sections: [],
    };
  },
  mounted() {
    $(this.$el).find("#sortable").sortable({
      items: ".sortable-section",
      update: this.onSortUpdate,
    });
    $(this.$el).find("#sortable1").sortable({
      items: ".sortable-section",
      update: this.onSortUpdate,
    });
  },
  methods: {
    onSortUpdate(event, ui) {
      // Ici, vous pourriez synchroniser l'ordre des sections si nécessaire,
      // mais si vous ne voulez pas stocker les sections dans un tableau,
      // vous pouvez laisser cette méthode vide.
    },
    // photo
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        this.fileName = file.name; // On stocke le nom du fichier sélectionné
        this.imageUrl = URL.createObjectURL(file); // On crée l'URL de l'objet pour l'image
      } else {
        this.fileName = null;
        this.imageUrl = null;
      }
    },
    // contact
    addContactLink() {
      this.contactLinks.push({ value: "" });
    },
    removeContactLink(index) {
      this.contactLinks.splice(index, 1);
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
    // sections
    addSection() {
      let section = {
        name: "",
        list: [],
        type: ["text", "list"],
        selectedType: "",
      };
      this.sections.push(section);
    },
    removeSection(index) {
      this.sections.splice(index, 1);
    },
    addSectionItem(list) {
      let item = {
        name: "",
        type: ["text", "tel", "email"],
        selectedType: "",
      };
      list.push(item);
    },
    removeSectionItem(list, index) {
      list.splice(index, 1);
    },
    // pdf
    generatePDF() {
      const element = document.getElementById("cv");
      const opt = {
        filename: "CV",
        image: { type: "bmp", quality: 0.98 },
        html2canvas: { scale: 1.5, useCORS: true },
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
  height: 99vh;
  margin: auto;
  margin-top: 0.5rem;
  overflow-y: auto;
  border: 1px solid var(--grey);
  width: 500px;
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

.sortable-section:hover {
  cursor: grab;
  background: rgba(0, 0, 0, 0.1);
}
</style>

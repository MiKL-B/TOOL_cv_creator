<template>
  <div id="container">
    <div id="left-panel">
      <h1>Profil</h1>
      <div class="field">
        <label for="photo">Photo</label>
        <input type="file" @change="handleFileUpload" accept="image/*" />
      </div>
      <div class="field">
        <label for="name">Name</label>
        <input id="name" type="text" placeholder="Name" v-model="name" />
      </div>
      <div class="field">
        <label for="firstname">Firstname</label>
        <input
          id="firstname"
          type="text"
          placeholder="Firstname"
          v-model="firstname"
        />
      </div>
      <div class="field">
        <label for="job">Job</label>
        <input id="job" type="text" placeholder="Job" v-model="job" />
      </div>
      <div class="field">
        <label for="pitch">Pitch</label>
        <textarea
          v-model="pitch"
          rows="5"
          placeholder="Your pitch here..."
        ></textarea>
      </div>
      <QualifForm
        name="experience"
        :qualifications="experiences"
        @add-qualification="addQualification(experiences)"
        @add-qualification-item="addItem"
        @remove-qualification="removeItem"
        @remove-qualification-item="removeItem"
      />
      <QualifForm
        name="formation"
        :qualifications="formations"
        @add-qualification="addQualification(formations)"
        @add-qualification-item="addItem"
        @remove-qualification="removeItem"
        @remove-qualification-item="removeItem"
      />

      <SectionForm
        :list="list1"
        @add-section="addSection"
        @remove-section="removeSection"
        @add-section-item="addItem"
        @remove-section-item="removeSectionItem"
      />
      <div class="field">
        <label for="color">Accent color</label>
        <input id="color" type="color" v-model="selectedColor" />
      </div>
      <div class="field">
        <label for="bgcolor">Background left panel color</label>
        <input
          id="bgcolor"
          type="color"
          v-model="selectedBackgroundLeftColor"
        />
      </div>
      <button id="generate-pdf" @click="generatePDF">Générer le PDF</button>
    </div>
    <div id="right-panel">
      <div id="cv">
        <div
          id="left-panel-cv"
          :style="{ backgroundColor: selectedBackgroundLeftColor }"
        >
          <section class="head sub-section">
            <div
              class="container-img"
              :style="{ border: '1px solid ' + selectedColor }"
              v-if="imageUrl !== null"
            >
              <div class="img">
                <img :src="imageUrl" placeholder="img here" />
              </div>
            </div>
            <div>
              <h1 class="name">
                <span class="firstname">{{ firstname }}</span>
                <span>{{ name }}</span>
              </h1>
              <h2 class="job" :style="{ color: selectedColor }">{{ job }}</h2>
            </div>
          </section>
          <div class="sortable" ref="list1">
            <SectionList :list="list1" :selectedColor="selectedColor" />
          </div>
        </div>
        <div id="right-panel-cv">
          <p
            class="text-profile"
            :style="{ '--dynamic-color': selectedColor }"
            v-if="pitch.length > 0"
          >
            {{ pitch }}
          </p>

          <div ref="list2" class="sortable">
            <SectionList :list="list2" :selectedColor="selectedColor" />
            <QualifList
              name="experience"
              :qualifications="experiences"
              :selectedColor="selectedColor"
            />
            <QualifList
              name="formation"
              :qualifications="formations"
              :selectedColor="selectedColor"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Sortable from "sortablejs";
import SectionList from "./components/SectionList.vue";
import SectionForm from "./components/SectionForm.vue";
import QualifForm from "./components/QualifForm.vue";
import QualifList from "./components/QualifList.vue";
export default {
  name: "App",
  components: {
    SectionList,
    SectionForm,
    QualifForm,
    QualifList,
  },
  data() {
    return {
      fileName: null,
      imageUrl: null,
      name: "",
      firstname: "",
      job: "",
      pitch: "",
      list1: [],
      list2: [],
      experiences: [],
      formations: [],
      selectedColor: "",
      selectedBackgroundLeftColor: "",
    };
  },
  mounted() {
    this.initSortable(this.$refs.list1);
    this.initSortable(this.$refs.list2);
  },
  methods: {
    addQualification(list) {
      let qualification = {
        name: "",
        dateFrom: "",
        dateTo: "",
        list: [],
      };
      list.push(qualification);
    },
    addItem(list) {
      list.push({ name: "" });
    },
    removeItem(data) {
      const [list, id] = data;
      list.splice(id, 1);
    },
    // sections
    addSection() {
      let section = {
        name: "",
        list: [],
      };

      this.list1.push(section);
    },
    removeSection(id) {
      this.list1.splice(id, 1);
    },
    initSortable(listElement) {
      new Sortable(listElement, {
        group: {
          name: "shared",
          pull: true,
          put: true,
        },
        animation: 150,
      });
    },

    // photo
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (!file) return;
      this.fileName = file.name;
      this.imageUrl = URL.createObjectURL(file);
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

      html2pdf().from(element).set(opt).save();
    },
  },
};
</script>
<style>
.sortable:hover {
  border: 1px dashed var(--grey);
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

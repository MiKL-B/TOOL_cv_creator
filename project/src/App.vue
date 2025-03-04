<template>
  <div id="container">
    <button @click="isOpen = !isOpen">Menu</button>
    <div id="left-panel" v-if="!isOpen">
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
        <input id="pitch" type="text" placeholder="Pitch" v-model="pitch" />
      </div>
      <FormSection
        :list="list1"
        @add-section="addSection"
        @remove-section="removeSection"
        @add-section-item="addSectionItem"
        @remove-section-item="removeSectionItem"
      />
      <input type="color" name="" v-model="selectedColor">

      <button id="generate-pdf" @click="generatePDF">Générer le PDF</button>
    </div>
    <div id="right-panel">
      <div id="cv">
        <div id="left-panel-cv" :style="{ backgroundColor: selectedColor }">
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
          <div class="sortable" ref="list1">
            <List :list="list1" />
          </div>
        </div>
        <div id="right-panel-cv">
          <p class="text-profile" v-if="pitch.length > 0">
            {{ pitch }}
          </p>
          <div ref="list2" class="sortable">
            <List :list="list2" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Sortable from "sortablejs";
import List from "./components/List.vue";
import FormSection from "./components/FormSection.vue";
export default {
  name: "App",
  components: {
    List,
    FormSection,
  },
  data() {
    return {
      isOpen: false,
      fileName: null,
      imageUrl: null,
      name: "",
      firstname: "",
      job: "",
      pitch: "",
      list1: [],
      list2: [],
      selectedColor:"",
    };
  },
  mounted() {
    this.initSortable(this.$refs.list1);
    this.initSortable(this.$refs.list2);
  },
  methods: {
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

    // sections
    addSection() {
      let section = {
        name: "",
        list: [],
        type: ["text", "list"],
        selectedType: "text",
      };

      this.list1.push(section);
    },
    removeSection(id) {
      this.list1.splice(id, 1);
    },
    addSectionItem(list) {
      let item = {
        name: "",
        type: ["text", "tel", "email"],
        selectedType: "text",
      };
      list.push(item);
    },
    removeSectionItem(data) {
      const [list, id] = data;
      list.splice(id, 1);
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

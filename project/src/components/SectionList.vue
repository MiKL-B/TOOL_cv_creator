<template>
  <div
    class="sub-section sortable-section"
    v-for="(section, index) in list"
    :key="index"
  >
    <h3 class="section-title">{{ section.name.toUpperCase() }}</h3>
    <ul v-if="section.selectedType === 'list'">
      <li v-for="item in section.list">
        <Phone v-if="item.selectedType === 'tel'" />
        {{ item.name }}
      </li>
    </ul>
    <div v-else-if="section.selectedType === 'text'">
      <p v-for="item in section.list">
        <Phone v-if="item.selectedType === 'tel'" />
        {{ item.name }}
      </p>
    </div>
    <div v-else-if="section.selectedType === 'experience'">
      <p
        v-for="item in section.list"
        style="display: flex; flex-direction: column"
      >
        <span style="font-weight: bold">{{ item.name.toUpperCase() }}</span>
        <span style="color: var(--grey)"
          >{{ item.dateFrom }} - {{ item.dateTo }}</span
        >
      </p>
    </div>
  </div>
</template>

<script>
import { Phone } from "lucide-vue-next";
export default {
  name: "SectionList",
  components: {
    Phone,
  },
  props: ["list"],
};
</script>

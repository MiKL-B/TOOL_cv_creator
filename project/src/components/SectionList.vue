<template>
  <div
    class="sub-section sortable-section"
    v-for="(section, index) in list"
    :key="index"
  >
    <h3
      class="section-title"
      :style="{
        color: selectedColor,
        borderBottom: '1px solid ' + selectedColor,
      }"
    >
      {{ section.name.toUpperCase() }}
    </h3>
    <div>
      <p v-for="item in section.list">
        {{ item.name }}
      </p>
    </div>
 
  </div>
</template>

<script>
export default {
  name: "SectionList",

  props: ["list", "selectedColor"],
};
</script>

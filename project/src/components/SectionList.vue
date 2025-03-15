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
        <span v-if="item.option === 'text'">{{ item.name }}</span>
        <span class="flex gap-4" v-if="item.option === 'tel'">
          <Phone />
          {{ item.name }}
        </span>
        <span class="flex gap-4" v-if="item.option === 'email'">
          <Mail />
          <a :style="{ color: selectedColor, borderBottom: '1px solid ' + selectedColor }" :href="'mailto:'+item.link">{{ item.link }}</a>
        </span>
        <span class="flex gap-4" v-if="item.option === 'linkedin'">
          <Linkedin />
          <a :style="{ color: selectedColor, borderBottom: '1px solid ' + selectedColor }" :href="'https://'+item.link" target="_blank">{{ item.link }}</a>
        </span>
        <span class="flex gap-4" v-if="item.option === 'github'">
          <Github />
          <a :style="{ color: selectedColor, borderBottom: '1px solid ' + selectedColor }" :href="'https://'+item.link" target="_blank">{{ item.link }}</a>
        </span>
        <span class="flex gap-4" v-if="item.option === 'link'">
          <Link />
          {{ item.name }}:
          <a :style="{ color: selectedColor, borderBottom: '1px solid ' + selectedColor }" :href="'https://'+item.link" target="_blank">{{ item.link }}</a>
        </span>
        <span class="flex gap-4" v-if="item.option === 'position'">
          <MapPin />
          {{ item.name }}
        </span>
        <span class="flex gap-4" v-if="item.option === 'vehicule'">
          <Car />
          {{ item.name }}
        </span>
        <ul v-if="item.option === 'item'">
          <li>{{ item.name }}</li>
        </ul>
      </p>
    </div>
 
  </div>
</template>

<script>
import { Phone,Mail,Linkedin,Github, MapPin,Car,Link } from 'lucide-vue-next';
export default {
  name: "SectionList",
  components:{
    Phone,
    Mail,
    Linkedin,
    Github,
    MapPin,
    Car,
    Link
  },
  props: ["list", "selectedColor"],
};
</script>
<style>
.flex{
  display: flex;
  align-items: center;
}
.gap-4{
  gap:0.5rem;
}
</style>
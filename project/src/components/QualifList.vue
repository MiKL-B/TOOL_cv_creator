<template>
	<div class="sub-section sortable-section" v-if="qualifications.length > 0">
		<h3 class="section-title" :style="{ color: selectedColor, borderBottom: '1px solid ' + selectedColor }">
			{{ name.toUpperCase() }}</h3>
		<div v-for="qualif in qualifications" style="margin-bottom:2rem">
			<p style="font-weight: bold">{{ qualif.name.toUpperCase() }}</p>
			<span style="color: var(--grey)" v-if="qualif.dateFrom !== '' || qualif.dateTo !== ''">
				{{ formatDate(qualif.dateFrom) }} - {{ formatDate(qualif.dateTo) }}
			</span>
			<ul>
				<li v-for="item in qualif.list">{{ item.name }}</li>
			</ul>
		</div>
	</div>
</template>

<script>
import dayjs from "dayjs";
import 'dayjs/locale/fr';
export default {
	name: "QualifList",
	props: ["name", "qualifications", "selectedColor"],
	computed: {
		// mydate() {
		// 	return dayjs(date).locale('fr').format('MMMM YYYY');
		// }
	},
	methods: {
		formatDate(date) {
			console.log(date)
			return dayjs(date).locale('fr').format('MMMM YYYY');
		}
	}

};
</script>

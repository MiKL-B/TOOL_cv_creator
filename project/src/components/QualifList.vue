<template>
	<div class="sub-section sortable-section">
		<h3 class="section-title">{{name.toUpperCase()}}</h3>
		<div v-for="qualif in qualifications">
			<p style="font-weight: bold">{{ qualif.name }}</p>
			<span
				style="color: var(--grey)"
				v-if="qualif.dateFrom !== '' && qualif.dateTo !== ''"
				>{{ qualif.dateFrom }} - {{ qualif.dateTo }}</span
			>
			<ul>
				<li v-for="item in qualif.list">{{ item.name }}</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	name: "QualifList",
	props:["name","qualifications"]
};
</script>

<template>
	<button @click="addQualification(list)">add {{ name }}</button>
	<div v-for="(qualif, index) in qualifications" :key="index">
		<input type="text" v-model="qualif.name" :placeholder="name + ' title...'"/>
		<input type="date" v-model="qualif.dateFrom" />
		<input type="date" v-model="qualif.dateTo" />
		<button @click="addQualificationItem(qualif.list)">addItem</button>
		<button @click="removeQualification(qualifications, index)">
			remove {{ name }}
		</button>
		<div v-for="(item, index) in qualif.list" :key="index">
			<input type="text" v-model="item.name" placeholder="item..." />
			<button @click="removeQualificationItem(qualif.list, index)">
				remove
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: "QualifForm",
	props: ["name", "qualifications"],
	emits: [
		"add-qualification",
		"add-qualification-item",
		"remove-qualification",
		"remove-qualification-item",
	],
	methods: {
		addQualification(list) {
			this.$emit("add-qualification", list);
		},
		addQualificationItem(list) {
			this.$emit("add-qualification-item", list);
		},
		removeQualification(list, id) {
			this.$emit("remove-qualification", [list, id]);
		},
		removeQualificationItem(list, id) {
			this.$emit("remove-qualification-item", [list, id]);
		},
	},
};
</script>

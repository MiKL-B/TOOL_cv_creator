<template>
	<div class="field">
		<h1>Section</h1>

		<div v-for="(section, index) in list" :key="index">
			<input v-model="section.name" placeholder="Section title..." />
			<button @click="removeSection(index)">Remove section</button>

			<button @click="addSectionItem(section.list)">add Item</button>

			<div v-for="(item, index) in section.list" :key="index">
				<input type="text" v-model="item.name" placeholder="item..."/>

				<button @click="removeSectionItem(section.list, index)">
					Remove item
				</button>
			</div>
		</div>
		<button @click="addSection">Add section</button>
	</div>
</template>

<script>
export default {
	name: "SectionForm",
	props: ["list"],
	emits: [
		"remove-section",
		"add-section",
		"add-section-item",
		"remove-section-item",
	],
	methods: {
		addSection() {
			this.$emit("add-section");
		},
		removeSection(id) {
			this.$emit("remove-section", id);
		},
		addSectionItem(list) {
			this.$emit("add-section-item", list);
		},
		removeSectionItem(list, id) {
			this.$emit("remove-section-item", [list, id]);
		},
	},
};
</script>

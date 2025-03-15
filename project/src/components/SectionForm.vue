<template>
	<div class="field">
		<h1>Section</h1>
		<div v-for="(section, index) in list" :key="index">
			<input v-model="section.name" placeholder="Section title..." />
			<button @click="removeSection(index)">Remove section</button>

			<button v-for="opt in options" @click="addSectionItem(section.list, opt)">add {{ opt }}</button>
			<div v-for="(item, index) in section.list" :key="index">
				<div v-if="item.option === 'link'">
					<input type="text" v-model="item.name" placeholder="name..." />
					<input type="text" v-model="item.link" placeholder="link..." />
				</div>
				<div v-else-if="item.option === 'linkedin' || item.option === 'github'">
					<input type="text" v-model="item.link" placeholder="link..." />
				</div>
				<input v-else-if="item.option === 'email'" v-model="item.link" type="email">
				<input v-else type="text" v-model="item.name" placeholder="item..." />
			
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
	data() {
		return {
			options: ["text", "tel", "linkedin", "github", "position", "vehicule", "item", "link", "email"]
		}
	},

	methods: {
		addSection() {
			this.$emit("add-section");
		},
		removeSection(id) {
			this.$emit("remove-section", id);
		},
		addSectionItem(list, opt) {
			this.$emit("add-section-item", [list, opt]);
		},
		removeSectionItem(list, id) {
			this.$emit("remove-section-item", [list, id]);
		},
	},
};
</script>

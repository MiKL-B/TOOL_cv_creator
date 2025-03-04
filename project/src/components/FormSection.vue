<template>
	<div class="field">
		<h1>Section</h1>
		<label for="sections">Sections</label>

		<div v-for="(section,index) in list" :key="index">
			<input v-model="section.name" placeholder="Entrer une valeur" />
			<button @click="removeSection(index)">Remove section</button>

			<button @click="addSectionItem(section.list)">add Item</button>

			<select v-model="section.selectedType">
				<option
					:value="item"
					v-for="item in section.type"
					:key="item.id"
				>
					{{ item }}
				</option>
			</select>

			<div v-for="(item, index) in section.list" :key="index">
				<input type="text" v-model="item.name" />
				<select v-model="item.selectedType">
					<option
						:value="subitem"
						v-for="subitem in item.type"
						:key="index"
					>
						{{ subitem }}
					</option>
				</select>
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
	name: "FormSection",
	props:["list"],
	emits:["remove-section","add-section","add-section-item","remove-section-item"],
	methods:{
		addSection(){
			this.$emit("add-section")
		},
		removeSection(id){
			this.$emit("remove-section",id)
		},
		addSectionItem(list){
			this.$emit("add-section-item",list)
		},
		removeSectionItem(list,id){
			this.$emit("remove-section-item",[list,id])
		}
	}
};
</script>

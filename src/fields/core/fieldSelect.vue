<template lang="pug">
	select.form-control(v-model="value", :disabled="disabled", :name="schema.inputName", :id="getFieldID(schema)")
		option(v-for="item in items", :value="getItemID(item)") {{ getItemName(item) }}
</template>

<script>
	import {isObject} from "lodash";
	import abstractField from "../abstractField";

	export default {
		mixins: [ abstractField ],

		computed: {
			selectOptions() {
				return this.schema.selectOptions || {};
			},

			items() {
				let values = this.schema.values;
				if (typeof(values) == "function") {
					return values.apply(this, [this.model, this.schema]);
				} else
					return values;
			}
		},

		methods: {
			getItemID(item) {
				if (isObject(item) && item.id)
					return item.id;

				return item;
			},

			getItemName(item) {
				if (isObject(item) && item.name)
					return item.name;

				return item;
			}
		}
	};
</script>


<style lang="sass">
</style>

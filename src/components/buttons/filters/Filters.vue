<template>
	<div class="filters-wrapper">
		<MyFilter
			v-for="(filter, index) in filters"
			:key="index"
			:inactive="! filter.active"
			type="button"
			@click="$emit('click', filter.id)"
		>
			{{ formatTitle(filter) }}
		</MyFilter>
	</div>
</template>

<script>
import MyFilter from "components/buttons/filters/MyFilter"

export default {
	name: "Filters",
	components:
		{
			MyFilter,
		},
	props:
		{
			/** An array of filters to be applied to some selection */
			filters: {
				required: true,
				type: Array,
			},
		},
	methods:
		{
			/**
			 * @param {object} filter - A self made filter object
			 * @returns {string} A formatted title
			 */
			formatTitle (filter)
			{
				return filter.title
			},
		},
}
</script>

<style scoped lang="less">
@import "~styles/styles";

.filters-wrapper {
	text-align: left;
	display: inline-flex;
	flex-wrap: wrap;

	&::-webkit-scrollbar {
		display: none;
	}
}
</style>

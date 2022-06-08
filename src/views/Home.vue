<template>
	<div class="home-wrapper">
		<AvailabilitySearch/>
	</div>
</template>

<script>
import AvailabilitySearch from "@/components/forms/AvailabilitySearch.vue"

export default {
	name: "Home",
	components:
		{
			AvailabilitySearch,
		},
	created: function()
	{
	},
}
</script>

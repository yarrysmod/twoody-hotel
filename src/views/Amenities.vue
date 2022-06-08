<template>
	<div class="amenities-wrapper">
		<h1>Amenities</h1>
		<AmenitiesTable/>
	</div>
</template>

<script>
import AmenitiesTable from "components/entities/amenities/AmenitiesTable"

export default {
	name: "Amenities",
	components:
		{
			AmenitiesTable,
		},
	created: function()
	{
	},
}
</script>

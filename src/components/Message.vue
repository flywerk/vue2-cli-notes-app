<template>
	<div class="message">
		<p>message component - {{ message }}</p>
	</div>
</template>

<script>
export default {
	props: {
		message: {
			type: String,
			required: true,
		},
	},
}
</script>

<template>
	<div class="tag">
		{{ tag }}
	</div>
</template>

<script>
export default {
	name: "SkillTag",
	props: {
		tag: {
			type: String,
			required: true,
		},
	},
};
</script>

<style lang="scss" scoped>
.tag {
	display: inline-block;
	background-color: var(--neutral-400);

	color: var(--primary-400);
	font-weight: bold;

	padding: 0.4em 0.5em 0.3em 0.5em;
	margin: 2rem 1.5rem 0 0;
}
</style>
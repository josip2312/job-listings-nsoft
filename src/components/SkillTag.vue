<template>
	<div class="tag" v-on="$listeners">
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
@import "@/assets/sass/_mixins";
@import "@/assets/sass/_variables";
.tag {
	display: inline-block;
	background-color: var(--neutral-400);

	color: var(--primary-400);
	font-weight: bold;

	line-height: 1.25;
	border-radius: var(-br);
	padding: 0.7em 0.7em 0.5em 0.7em;
	margin-top: 2rem;
	margin: 2rem 1.5rem 0 0;

	cursor: pointer;
	transition: background-color 200ms ease-in-out, color 200ms ease-in-out;

	&:hover {
		background-color: var(--primary-400);
		color: var(--neutral-300);
	}

	@include mq-min($v-14) {
		margin-top: 0;
	}
}
</style>
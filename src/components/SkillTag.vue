<template>
	<div v-on="$listeners" :class="{ 'tag-filter': isFilter }" class="tag">
		<span class="tag-text">
			{{ tag }}
		</span>
		<button
			v-if="isFilter"
			class="tag-remove"
		>
			<img src="@/assets/images/icon-remove.svg" alt="" />
		</button>
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
		isFilter: {
			type: Boolean,
			default: false,
		},
	},
};
</script>

<style lang="scss" scoped>
.tag {
	display: inline-block;

	color: var(--primary-400);
	font-weight: bold;
	line-height: 1.25;

	background-color: var(--neutral-400);
	border-radius: var(--br);
	padding: 0.7em 0.7em 0.6em 0.7em;
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
//when the tag is a filter
.tag-filter {
	display: flex;
	justify-content: space-between;

	padding: 0;
	margin-top: 1.5rem;

	&:hover {
		background-color: var(--neutral-400);
		color: var(--primary-400);
	}

	.tag-text {
		display: inline-block;
		padding: 0.6em 0.6em 0.5em 0.6em;
	}

	.tag-remove {
		flex-shrink: 0;

		border-radius: 0 0.5rem 0.5rem 0;
		background-color: var(--primary-400);
		padding: 0 1rem;

		cursor: pointer;
		transition: background-color 200ms ease-in-out;
		img {
			width: 1.5rem;
		}

		&:hover {
			background-color: var(--neutral-600);
		}
	}
}
</style>

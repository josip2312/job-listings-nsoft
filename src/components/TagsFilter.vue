<template>
	<transition name="fade" mode="out-in">
		<div class="filter" v-if="isFilterChosen">
			<transition-group name="tag-appear" tag="div" class="filter-items">
				<SkillTag
					v-for="tag in filterTags"
					:key="tag"
					:tag="tag"
					:isFilter="true"
					@remove-filter-tag="$emit('remove-filter-tag', $event)"
				/>
			</transition-group>
			<button class="clear" @click="$emit('clear-filters')">Clear</button>
		</div>
	</transition>
</template>

<script>
import SkillTag from "@/components/SkillTag";
export default {
	name: "TagFilter",
	components: {
		SkillTag,
	},
	props: {
		filterTags: {
			type: Array,
			required: true,
		},
		isFilterChosen: {
			type: Boolean,
			required: true,
		},
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/sass/_transitions";

.filter {
	position: absolute;
	top: -4rem;
	z-index: 100;

	width: 90%;
	max-width: 140rem;
	margin: 0 auto;

	display: flex;
	align-items: center;
	justify-content: space-between;

	padding: 1.5rem 2rem 3rem 2rem;
	background-color: var(--white);
	box-shadow: var(--box-shadow);
	border-radius: var(--br);

	@include mq-min($v-10) {
		top: -4.5rem;
		width: 85%;
		padding: 1.5rem 5rem 3rem 5rem;
	}

	&-items {
		display: flex;
		flex-wrap: wrap;
	}

	.clear {
		color: var(--neutral-500);
		font-weight: bold;

		padding: 0;
		margin-top: 1.5rem;

		cursor: pointer;
		&:hover {
			color: var(--primary-400);
			text-decoration: underline;
		}
	}
}
</style>
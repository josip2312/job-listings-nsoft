<template>
	<main class="jobs-list">
		<div class="container">
			<TagsFilter
				:isFilterChosen="isFilterChosen"
				:filterTags="filterTags"
				@remove-filter-tag="removeFilterTag"
				@clear-filters="clearFilters"
			/>

			<div v-if="isLoading" class="loading">Loading...</div>
			<div v-if="error !== null" class="error">{{ error }}</div>

			<transition-group
				v-if="!isLoading && error === null"
				name="fade-list"
				tag="section"
				class="cards spacing"
				:class="{
					translate: isFilterChosen,
					'increase-translate': multipleFiltersChosen,
				}"
			>
				<JobCard
					v-for="job in filteredJobs"
					:key="job.id"
					:job="job"
					@add-new-filter="addNewFilter"
				/>
			</transition-group>
		</div>
	</main>
</template>

<script>
import TagsFilter from "./TagsFilter.vue";
import JobCard from "./JobCard.vue";

export default {
	name: "JobsList",
	components: {
		JobCard,
		TagsFilter,
	},
	data() {
		return {
			filterTags: [],

			isLoading: false,
			error: null,
			jobs: [],
		};
	},
	computed: {
		filteredJobs() {
			return this.jobs.filter((job) => {
				let jobTags = [
					job.role,
					job.level,
					...job.languages,
					...job.tools,
				];
				if (this.isFilterChosen) {
					return this.filterTags.every((tag) =>
						jobTags.includes(tag)
					);
				}
				return job;
			});
		},
		isFilterChosen() {
			return this.filterTags.length > 0;
		},
		multipleFiltersChosen() {
			return this.filterTags.length > 2;
		},
	},
	async mounted() {
		this.fetchJobs();
	},

	methods: {
		addNewFilter(tag) {
			if (!this.filterTags.includes(tag)) this.filterTags.push(tag);
		},
		clearFilters() {
			this.filterTags = [];
		},
		removeFilterTag(tag) {
			this.filterTags = this.filterTags.filter(
				(filterTag) => filterTag !== tag
			);
		},
		// if it was a real http request, loading and error states
		// should be handled
		async fetchJobs() {
			try {
				this.error = null;
				this.isLoading = true;
				const res = await fetch("/data.json");
				const data = await res.json();
				this.jobs = data;
				this.isLoading = false;
			} catch (error) {
				this.isLoading = false;
				this.error = "Something went wrong";
				console.error(error);
			}
		},
	},
};
</script>

<style lang="scss" scoped>
//animations
.fade-list-enter,
.fade-list-leave-to {
	opacity: 0;
}
.fade-list-leave-active {
	position: absolute;
}

.loading,
.error {
	font-size: 2rem;
	color: var(--neutral-500);
}

.jobs-list {
	position: relative;
	padding: 7.5rem 0;
}

@keyframes appear {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}
.cards {
	--spacer: 5rem;
	animation: appear 500ms ease-in-out;

	transform: translateY(0);
	transition: transform 300ms ease-in-out;
}

.translate {
	transform: translateY(5rem);
	padding-bottom: 7.5rem;
}
.increase-translate {
	@include mq-max($v-6) {
		transform: translateY(10rem);
	}
}
</style>
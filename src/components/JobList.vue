<template>
	<main class="job-list">
		<div class="container spacing">
			<div class="filter">
				<div class="filter-items">
					<SkillTag
						v-for="(tag, index) in tagFilters"
						:key="index"
						:tag="tag"
					/>
				</div>
				<span class="clear">Clear</span>
			</div>
			<JobCard
				v-for="job in filteredJobs"
				:key="job.id"
				:job="job"
				@filter-by-tag="filterByTag"
			/>
		</div>
	</main>
</template>

<script>
import JobCard from "./JobCard.vue";
import SkillTag from "./SkillTag.vue";

export default {
	name: "JobList",
	components: {
		JobCard,
		SkillTag,
	},
	data() {
		return {
			tagFilters: [],

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
				if (this.tagFilters.length > 0) {
					return this.tagFilters.every((tag) =>
						jobTags.includes(tag)
					);
				}
				return job;
			});
		},
	},

	methods: {
		filterByTag(tag) {
			this.tagFilters.push(tag);
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
			} catch (error) {
				this.isLoading = false;
				this.error = "Something went wrong";
				console.error(error);
			}
		},
	},
	async mounted() {
		this.fetchJobs();
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/sass/_mixins";
@import "@/assets/sass/_variables";
.job-list {
	position: relative;
	padding: 7.5rem 0;
}
.container {
	--spacer: 5rem;
}
.filter {
	position: absolute;
	top: -3rem;
	z-index: 100;

	width: 90%;
	max-width: 140rem;
	margin: 0 auto;
	padding: 3rem;

	background-color: var(--white);
	box-shadow: var(--box-shadow);
	border-radius: var(--br);

	display: flex;
	align-items: center;
	justify-content: space-between;

	@include mq-min($v-10) {
		width: 85%;
	}
}
</style>
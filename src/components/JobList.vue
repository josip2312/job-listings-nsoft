<template>
	<main class="job-list">
		<div class="container spacing">
			<JobCard v-for="job in jobs" :key="job.id" :job="job" />
		</div>
	</main>
</template>

<script>
import JobCard from "./JobCard.vue";

export default {
	name: "JobList",
	components: {
		JobCard,
	},
	data() {
		return {
			isLoading: false,
			error: null,
			jobs: [],
		};
	},
	/* computed: {
		filteredJobs() {
            
			const newArr = this.jobs.map(({id, company, logo,new, featured, position, role, }) => {
				return {
					id: job.id,
                    company: job.company,
                    logo:
				};
			});
			console.log(newArr);
			return newArr;
		},
	}, */

	methods: {
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
.job-list {
	padding: 7.5rem 0;
}
.container {
	--spacer: 6rem;
}
</style>
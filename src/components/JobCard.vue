<template>
	<article class="card">
		<div class="avatar">
			<img :src="jobLogo" :alt="job.company" />
		</div>
		<div class="content">
			<div class="info">
				<div class="info-company">
					{{ job.company }}
				</div>
				<div class="info-new" v-if="job.new">New!</div>
				<div class="info-new" v-if="job.featured">Featured</div>
				<div class="info-position">{{ job.position }}</div>
				<div class="info-posted-at">
					{{ job.postedAt }}
				</div>
				<div class="info-contract">
					{{ job.contract }}
				</div>
				<div class="info-location">
					{{ job.location }}
				</div>
			</div>
			<div class="tags">
				{{ jobTags }}
			</div>
		</div>
	</article>
</template>

<script>
export default {
	name: "JobCard",
	props: {
		job: {
			type: Object,
			required: true,
		},
	},
	computed: {
		jobLogo() {
			const logoName = this.job.logo.split("/")[2];
			return require(`@/assets/images/${logoName}`);
		},
		jobTags() {
			return [
				this.job.role,
				this.job.level,
				...this.job.languages,
				...this.job.tools,
			];
		},
	},
};
</script>

<style lang="scss" scoped>
</style>
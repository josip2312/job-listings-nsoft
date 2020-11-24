<template>
	<article class="card" :class="{ featured: job.featured }">
		<div class="avatar">
			<img :src="jobLogo" :alt="job.company" />
		</div>
		<div class="content">
			<div class="info spacing">
				<div class="info-company">
					{{ job.company }}
				</div>
				<div class="info-new" v-if="job.new">New!</div>
				<div class="info-featured" v-if="job.featured">Featured</div>

				<h3 class="info-position heading-3">{{ job.position }}</h3>
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
				<SkillTag
					v-for="(tag, index) in jobTags"
					:key="index"
					:tag="tag"
					@click="filterByTag(tag)"
				/>
			</div>
		</div>
	</article>
</template>

<script>
import SkillTag from "./SkillTag.vue";
export default {
	components: { SkillTag },
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
	methods: {
		filterByTag(tag) {
			this.$emit("filter-by-tag", tag);
		},
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/sass/_mixins";
@import "@/assets/sass/_variables";
.card {
	position: relative;
	padding: 3.5rem 2.25rem;
	background-color: var(--white);

	box-shadow: var(--box-shadow);
	border-radius: var(--br);
	@include mq-min($v-14) {
		padding-left: 3.5rem;
		padding-right: 2.5rem;
		display: flex;
		align-items: center;
	}
}
//class if job is featured
.featured {
	border-left: 0.6rem solid var(--primary-400);
}

.avatar {
	position: absolute;
	top: -3rem;

	img {
		width: 6rem;
	}
	@include mq-min($v-14) {
		position: relative;
		top: 0;
		img {
			width: 11rem;
		}
	}
}

.content {
	@include mq-min($v-14) {
		flex: 1;
		margin-left: 2.25rem;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
}
.info {
	--spacer: 1.5rem;

	border-bottom: 1px solid var(--neutral-500);
	padding-bottom: 2rem;
	@include mq-min($v-14) {
		border-bottom: none;
		padding-bottom: 0;
	}

	&-company,
	&-new,
	&-featured {
		display: inline-block;
		@include mq-min($v-14) {
			margin-top: 0;
		}
	}
	&-company {
		color: var(--primary-400);
		font-weight: bold;
		margin-right: 1.5rem;
	}
	&-new {
		background-color: var(--primary-400);
		padding: 0.8em 0.8em 0.5em 0.8em;
		border-radius: 5rem;

		color: var(--neutral-300);
		text-align: center;
		text-transform: uppercase;
		font-weight: bold;
		font-size: 1.2rem;
		line-height: 1;

		margin-right: 0.75rem;
	}
	&-featured {
		@extend .info-new;
		margin-right: 0;
		background-color: var(--neutral-600);
	}

	&-position {
		cursor: pointer;

		transition: color 200ms ease-in-out;
		&:hover {
			color: var(--primary-400);
		}
	}

	&-posted-at,
	&-contract,
	&-location {
		position: relative;
		display: inline-block;
		color: var(--neutral-500);
	}
	&-posted-at::after,
	&-contract::after {
		content: "";
		display: inline-block;
		width: 0.4rem;
		height: 0.4rem;
		border-radius: 50%;
		background-color: var(--neutral-500);

		position: absolute;
		right: -1.3rem;
		top: 40%;
		transform: translateY(-40%);
	}
	&-posted-at {
		margin-right: 2.5rem;
	}
	&-contract {
		margin-right: 2.5rem;
	}
	&-location {
	}
}

.tags {
}
</style>
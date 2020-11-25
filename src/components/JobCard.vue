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
				<div v-if="job.new" class="info-new">New!</div>
				<div v-if="job.featured" class="info-featured">Featured</div>

				<h3 class="info-position heading-3">
					{{ job.position }}
				</h3>

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
					v-for="tag in jobTags"
					:key="tag"
					:tag="tag"
					@click="addNewFilter(tag)"
				/>
			</div>
		</div>
	</article>
</template>

<script>
import SkillTag from "./SkillTag.vue";
export default {
	name: "JobCard",
	components: { SkillTag },
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
		addNewFilter(tag) {
			this.$emit("add-new-filter", tag);
		},
	},
};
</script>

<style lang="scss" scoped>
.card {
	position: relative;

	padding: 3.5rem 2.25rem;
	background-color: var(--white);
	box-shadow: var(--box-shadow);
	border-radius: var(--br);

	transition: opacity 400ms ease, transform 400ms ease;

	@include mq-min($v-14) {
		display: flex;
		align-items: center;

		padding-left: 3.5rem;
		padding-right: 2.5rem;
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
		width: 6.5rem;
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
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-left: 2.25rem;
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
		margin-right: 1.5rem;
		color: var(--primary-400);
		font-weight: bold;
	}
	&-new {
		background-color: var(--primary-400);
		padding: 0.8em 0.8em 0.6em 0.8em;
		border-radius: 5rem;

		color: var(--neutral-300);
		text-align: center;
		text-transform: uppercase;
		font-weight: bold;
		font-size: 1.3rem;
		line-height: 1;

		margin-right: 0.75rem;
	}
	&-featured {
		@extend .info-new;
		background-color: var(--neutral-600);
		margin-right: 0;
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
		position: absolute;
		right: -1.3rem;
		top: 47.5%;
		transform: translateY(-47.5%);

		display: inline-block;
		width: 0.3rem;
		height: 0.3rem;
		border-radius: 50%;
		background-color: var(--neutral-500);
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
</style>
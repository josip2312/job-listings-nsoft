<template>
	<div id="app">
		<TheHeader />
		<JobList />
	</div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
import JobList from "./components/JobList.vue";
export default {
	name: "App",
	components: { TheHeader, JobList },
};
</script>

<style lang="scss">
@import "@/assets/sass/main.scss";
</style>

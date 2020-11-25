<template>
	<div id="app">
		<TheHeader />
		<JobsList />
	</div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
import JobsList from "./components/JobsList.vue";

export default {
	name: "App",
	components: { TheHeader, JobsList },
};
</script>

<style lang="scss">
@import "@/assets/sass/main.scss";
</style>

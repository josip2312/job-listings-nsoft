<template>
	<div id="app">
		<TheHeader />
	</div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
export default {
	name: "App",
	components: { TheHeader },

	async mounted() {
		const res = await fetch("/data.json");
		const data = await res.json();
		console.log(data);
	},
};
</script>

<style lang="scss">
@import "@/assets/sass/main.scss";
</style>

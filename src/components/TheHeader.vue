<template>
	<header class="header">
		<div class="container"></div>
	</header>
</template>

<script>
export default {
	name: "TheHeader",
};
</script>

<style lang="scss" scoped>
.header {
	background-image: url("../assets/images/bg-header-mobile.svg");
	background-color: var(--primary-400);
	min-height: 15vh;
	background-position: center;
	background-size: cover;
	background-repeat: no-repeat;
}
</style>
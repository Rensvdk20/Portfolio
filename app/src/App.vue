<template>
	<!-- <header>
		<div class="wrapper">
			<nav>
				<RouterLink to="/">Home</RouterLink>
			</nav>
		</div>
	</header> -->

	<RouterView />
	<Footer />
</template>

<style lang="scss" scoped>
nav {
	position: absolute;
	display: flex;
	gap: 30px;
	font-size: 1.2rem;
	margin: 20px;

	a:hover {
		color: darken(white, 10);
	}
}
</style>
<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
import Footer from "./components/utilities/Footer.vue";
</script>

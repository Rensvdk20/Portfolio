<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
	<header>
		<div class="wrapper">
			<nav>
				<RouterLink to="/">Home</RouterLink>
				<RouterLink to="/about">About</RouterLink>
			</nav>
		</div>
	</header>

	<RouterView />
</template>

<style scoped>
nav {
	position: absolute;
	display: flex;
	gap: 30px;
	font-size: 1.2rem;
	margin: 20px;
}
</style>

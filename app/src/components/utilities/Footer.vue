<template>
	<footer>
		<div class="pages">
			<router-link to="/">Home</router-link>
			<router-link to="/projects">Projects</router-link>
			<router-link to="/contact">Contact</router-link>
		</div>
		<div class="copyright">@ {{ year }} - Rens van der Kemp</div>
	</footer>
</template>
<style scoped lang="scss">
footer {
	padding: 80px 0;
	background-color: $secondary;
	text-align: center;

	.pages {
		display: flex;
		justify-content: center;
		gap: 30px;
		font-size: 1.2rem;
		margin: 20px;

		a:hover {
			color: darken(white, 10);
		}
	}
}

@media #{$xs} {
	footer {
		padding: 40px 10px;

		.pages {
			flex-direction: column;
			gap: 10px;
		}
	}
}
</style>
<script setup lang="ts">
let year = new Date().getFullYear();
</script>

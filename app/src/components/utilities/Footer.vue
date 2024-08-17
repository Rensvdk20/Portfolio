<template>
	<footer>
		<div class="pages">
			<p @click="scrollTo('header')">Home</p>
			<p @click="scrollTo('project-item')">Projects</p>
			<p @click="scrollTo('contact')">Contact</p>
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

		p:hover {
			cursor: pointer;
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

const scrollTo = (className: string) => {
	const element = document.querySelector(`.${className}`);
	if (element) {
		element.scrollIntoView({ behavior: "smooth" });
	}
};
</script>

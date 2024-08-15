<template>
	<div class="about">
		<div class="about-text">
			<h2>About me</h2>
			<p>
				I’m a developer based around Rotterdam, The Netherlands. I’ve been coding since
				2018, and I’m passionate about creating applications that help make people’s life
				easier. I’m dedicated to build high-performance, secure applications that ensure a
				seamless experience for the end user.
			</p>
		</div>
		<div class="about-img">
			<img src="/src/assets/images/programming.svg" />
		</div>
	</div>
</template>

<style lang="scss" scoped>
.about {
	display: flex;
	justify-content: center;
	align-items: center;
	gap: 100px;
	background-color: $secondary;
	padding: 80px 0;

	&-text {
		max-width: 30%;
		font-size: 1.2rem;
	}
}

@media #{$lg} {
	.about {
		flex-direction: column;

		&-text {
			max-width: 80%;
		}

		&-img {
			text-align: center;

			img {
				width: 80%;
			}
		}
	}
}
</style>

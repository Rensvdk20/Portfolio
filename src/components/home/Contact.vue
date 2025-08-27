<template>
	<div class="contact">
		<p>Contact?</p>
		<p>
			Send me an
			<a
				href="mailto:&#114;&#101;&#110;&#115;&#118;&#100;&#107;&#064;&#103;&#109;&#097;&#105;&#108;&#046;&#099;&#111;&#109;"
				>email!</a
			>
		</p>
	</div>
</template>
<style scoped lang="scss">
.contact {
	padding: 80px;

	p {
		text-align: center;
		font-size: 2rem;
		font-weight: 700;
		margin: 0;

		&:nth-of-type(1) {
			margin-bottom: 25px;
		}
	}

	a {
		cursor: pointer;
		text-decoration: underline;
		position: relative;
		display: inline-block;
		text-underline-offset: 3px;

		&:hover {
			text-decoration: none;

			&::after {
				content: "";
				position: absolute;
				left: 0;
				right: 0;
				bottom: 1px;
				height: 4px;
				background: linear-gradient(270deg, darken($primary, 8), darken($primary, 20));
				background-size: 400% 400%;
				animation: MoveGradBackground 2s ease infinite;
			}
		}
	}

	@keyframes MoveGradBackground {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}
}

@media #{$lg} {
	.contact {
		padding: 80px 10px;
	}
}
</style>
<script setup lang="ts"></script>

<template>
	<div class="header">
		<h1 class="header-text">Hi, I’m Rens Fullstack Webdeveloper</h1>
		<div class="header-image">
			<img
				src="/src/assets/images/profile.png"
				width="450px"
				alt="Profile Picture"
				draggable="false"
				:style="movePicWithMouse"
			/>
			<div class="header-shapes">
				<div class="shape-block-container">
					<div class="shape-block" ref="shapeBlock" :style="moveShapeWithMouse"></div>
				</div>
				<div class="shape-circle-big-container">
					<div
						class="shape-circle-big"
						ref="shapeCircleBig"
						:style="moveShapeWithMouse"
					></div>
				</div>
				<div class="shape-circle-small-container">
					<div
						class="shape-circle-small"
						ref="shapeCircleSmall"
						:style="moveShapeWithMouse"
					></div>
				</div>
			</div>
		</div>
	</div>
	<div class="about"></div>
</template>

<style lang="scss">
.header {
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	gap: 250px;

	&-text {
		max-width: 300px;
		font-size: 3rem;
		font-weight: 300;
	}

	&-image {
		position: relative;
	}

	.shape-block {
		width: 45px;
		height: 450px;
		background-color: $secondary;
		transform: rotate(15deg);

		&-container {
			position: absolute;
			z-index: -1;
			top: -100px;
			left: 20px;
			animation: float 6s infinite ease-in-out;
		}
	}

	.shape-circle-big {
		width: 150px;
		height: 150px;
		background-color: $secondary;
		border-radius: 50%;

		&-container {
			position: absolute;
			top: 300px;
			right: -100px;
			animation: float 6s infinite ease-in-out;
		}
	}

	.shape-circle-small {
		width: 100px;
		height: 100px;
		background-color: $secondary;
		border-radius: 50%;

		&-container {
			position: absolute;
			top: 200px;
			right: 0;
			animation: float 6s infinite ease-in-out;
		}
	}
}

@keyframes float {
	0% {
		transform: translateY(0);
	}

	50% {
		transform: translateY(-15px);
	}

	100% {
		transform: translateY(0);
	}
}
</style>

<script>
export default {
	name: "LeaningShape",
	data() {
		return {
			offsetX: 0,
			offsetY: 0
		};
	},
	computed: {
		moveShapeWithMouse() {
			console.log(this.offsetX);
			return {
				transform: `translate(${this.offsetX}px, ${this.offsetY}px) rotate(15deg)`
			};
		},
		movePicWithMouse() {
			return {
				transform: `translate(${this.offsetX / 4}px, ${this.offsetY / 4}px) rotate(${3 + -this.offsetX / 10}deg)`
			};
		}
	},
	methods: {
		handleMouseMove(event) {
			const shape = this.$refs.shapeBlock;
			if (shape) {
				const shapeRect = shape.getBoundingClientRect();
				const shapeCenterX = shapeRect.left + shapeRect.width / 2;
				const shapeCenterY = shapeRect.top + shapeRect.height / 2;

				const mouseX = event.clientX;
				const mouseY = event.clientY;

				const deltaX = mouseX - shapeCenterX;
				const deltaY = mouseY - shapeCenterY;

				const maxOffset = 5;
				const distance = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
				const normalizedDistance = Math.min(distance / 1000, 1);

				this.offsetX = (deltaX / distance) * maxOffset * normalizedDistance;
				this.offsetY = (deltaY / distance) * maxOffset * normalizedDistance;
			}
		}
	},
	mounted() {
		window.addEventListener("mousemove", this.handleMouseMove);
	},
	beforeDestroy() {
		window.removeEventListener("mousemove", this.handleMouseMove);
	}
};
</script>

<template>
	<div class="header">
		<h1 class="header-text">Hi, I’m Rens A Fullstack Webdeveloper</h1>
		<h1 class="header-text-mobile">
			Hi, I’m Rens<br />
			A Fullstack Webdeveloper
		</h1>
		<div class="header-image">
			<img
				src="/assets/images/profile.png"
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
	<About />
	<ProjectItem v-for="project in projects" :key="project.id" :project="project" />
	<Contact />
</template>

<style scoped lang="scss">
.header {
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	gap: 250px;

	&-text {
		max-width: 300px;
		font-weight: 300;

		&-mobile {
			display: none;
			font-weight: 300;
		}
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

@media #{$xxl} {
	.header {
		gap: 200px;
	}
}

@media #{$xl} {
	.header {
		scale: 0.8;
	}
}

@media #{$lg} {
	.header {
		flex-direction: column-reverse;
		gap: 0;
		scale: 1;

		&-image {
			scale: 0.8;
		}

		&-text {
			display: none;

			&-mobile {
				display: block;
				margin: 0 45px;
				z-index: 100;
				text-align: center;
			}
		}
	}
}

@media #{$sm} {
	.header {
		gap: 35px;

		&-shapes {
			display: none;
		}

		&-image {
			scale: 1;
			text-align: center;

			img {
				max-width: 80%;
			}
		}

		&-text-mobile {
			font-size: 240%;
		}
	}
}
</style>

<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from "vue";
import type { IProjectItem } from "@/interfaces/IProjectItem";
import ProjectItem from "@/components/home/ProjectItem.vue";
import Contact from "@/components/home/Contact.vue";
import About from "./About.vue";

const offsetX = ref(0);
const offsetY = ref(0);
const projects = <IProjectItem[]>[
	{
		id: "1",
		name: "Imeardle",
		languages: "Nextjs - Prisma - Scss",
		description:
			"A personal project of mine build with Next 13. It’s all about guessing a song by only hearing a few seconds of a song. Create your own and imagine a new heardle",
		image: "/assets/images/projects/Imeardle.jpg",
		link: "https://github.com/Rensvdk20/Imeardle",
		color: "#EB3372"
	},
	{
		id: "2",
		name: "Foodwise",
		languages: "C# - Rest API - Scss",
		description:
			"Website for my university to not waste food, by using the Too Good To Go concept. Students can reserve food boxes at specific timeslots and pick them up at the selected canteen.",
		image: "/assets/images/projects/Foodwise.jpg",
		link: "",
		color: "#C7002B"
	}
];

// Computed properties
const moveShapeWithMouse = computed(() => {
	return {
		transform: `translate(${offsetX.value}px, ${offsetY.value}px) rotate(15deg)`
	};
});

const movePicWithMouse = computed(() => {
	return {
		transform: `translate(${offsetX.value / 4}px, ${offsetY.value / 4}px) rotate(${-offsetX.value / 10}deg)`
	};
});

// Methods
const handleMouseMove = (event: MouseEvent) => {
	const shape = document.querySelector(".shape-block") as HTMLElement;
	if (shape) {
		const shapeRect = shape.getBoundingClientRect();
		const shapeCenterX = shapeRect.left + shapeRect.width / 2;
		const shapeCenterY = shapeRect.top + shapeRect.height / 2;

		const mouseX = event.clientX;
		const mouseY = event.clientY;

		const deltaX = mouseX - shapeCenterX;
		const deltaY = mouseY - shapeCenterY;

		const maxOffset = 10;
		const distance = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
		const normalizedDistance = Math.min(distance / 1000, 1);

		offsetX.value = (deltaX / distance) * maxOffset * normalizedDistance;
		offsetY.value = (deltaY / distance) * maxOffset * normalizedDistance;
	}
};

onMounted(() => {
	window.innerWidth >= 992 ? window.addEventListener("mousemove", handleMouseMove) : null;
});

onBeforeUnmount(() => {
	window.innerWidth >= 992 ? window.removeEventListener("mousemove", handleMouseMove) : null;
});
</script>
